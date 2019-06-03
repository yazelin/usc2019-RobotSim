## 自動化專案實作加分題

<iframe width="560" height="315" src="https://www.youtube.com/embed/gm2w0d_TMHY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


```cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace AxisControler
{
	public partial class Form1 : Form
	{
		List<ButtonControler> controlers = new List<ButtonControler>();
		ClientExample client = new ClientExample();

		private string distancePositive = "10";
		private string distanceNegative = "-10";

		public Form1()
		{
			InitializeComponent();

			client.UpDataIn += Client_UpData;
			client.SatatusChanged += Client_StatusChanged;

			controlers.AddRange(new List<ButtonControler>() { buttonControler1, buttonControler2, buttonControler3, buttonControler4, buttonControler5, buttonControler6 });

			foreach (var item in controlers)
			{
				item.AddButtonClick += AxisControler1_OnAddButtonClick;
				item.DelButtonClick += AxisControler1_OnDelButtonClick;
			}

		}

		private void Client_StatusChanged(object sender, StatuChangeEventArgs e)
		{
			UIThread(this, () =>
			{
				foreach (var item in controlers)
				{
					item.Enabled = e.idle;                  //if robot idle, close button
				}
			});
		}

		private void AxisControler1_OnDelButtonClick(object sender, EventArgs e)
		{
			var axis = (sender as ButtonControler).AxisID;
			var dataSend = "<Distance><Axis Angle =\"" + distanceNegative + "\">" + axis + "</Axis></Distance>";
			client.Send(dataSend);
		}

		private void AxisControler1_OnAddButtonClick(object sender, EventArgs e)
		{
			var axis = (sender as ButtonControler).AxisID;
			var dataSend = "<Distance><Axis Angle =\"" + distancePositive + "\">" + axis + "</Axis></Distance>";
			client.Send(dataSend);
		}

		private void Client_UpData(object sender, UpDataInEventArgs e)
		{
			UIThread(this, () =>
			{
				buttonControler1.CurrentPosition = e.A1.ToString();
				buttonControler2.CurrentPosition = e.A2.ToString();
				buttonControler3.CurrentPosition = e.A3.ToString();
				buttonControler4.CurrentPosition = e.A4.ToString();
				buttonControler5.CurrentPosition = e.A5.ToString();
				buttonControler6.CurrentPosition = e.A6.ToString();
			});
		}

		private static void UIThread(Control control, Action code)
		{
			if (control.InvokeRequired)				//call otehr threads
			{
				control.BeginInvoke(code);
			}
			else
			{
				code.Invoke();
			}
		}

		private void ClientStart_Click(object sender, EventArgs e)
		{
			client.Start("192.168.1.147", 54600);
		}

		private void ClientStop_Click(object sender, EventArgs e)
		{
			client.Stop();
		}
	}
}
  ```

```c#
using System;
using System.IO;
using System.Net.Sockets;
using System.Threading;
using System.Threading.Tasks;
using System.Xml;

namespace AxisControler
{
	class ClientExample
	{
		TcpClient myClient;         //建立TcpClient
		public event EventHandler<UpDataInEventArgs> UpDataIn;
		public event EventHandler<StatuChangeEventArgs> SatatusChanged;
		private string sendData = string.Empty;
		private bool idle;
		private bool beforeIdle = false;

		public ClientExample() { }

		public void Start(string ip, int port)
		{
			if (myClient != null)        
			{
				return;
			}
			myClient = new TcpClient(ip, port);  

			Task.Run(() => ClientService());      //task run in other thread
		}

		public void Send(string data)
		{
			sendData = data;
		}

		private void ClientService()
		{
			while (true)
			{

				try
				{

					if (myClient != null)           //mtClient has entity
					{
						StreamReader streamReader = new StreamReader(myClient.GetStream());
						StreamWriter streamWriter = new StreamWriter(myClient.GetStream());

						while (myClient.Connected)
						{
							if (sendData != string.Empty) 
							{
								streamWriter.WriteLine(sendData);       
								streamWriter.Flush();                   //send "sendData"
								Console.WriteLine("Client To Server : " + sendData);

								var data = streamReader.ReadLine();     //read "Confirm"
								Console.WriteLine("From Server : " + data);

								sendData = string.Empty;
							}

							var dataPosition = streamReader.ReadLine();			//read position and idle
							Console.WriteLine("From Server : " + dataPosition);

							XmlDocument xmlDocument = new XmlDocument();
							xmlDocument.LoadXml(dataPosition);      //dataPosition set in xmlDocument

							var positionA1 = xmlDocument.SelectSingleNode("/Position/A1").InnerText;    //take Xml content
							var positionA2 = xmlDocument.SelectSingleNode("/Position/A2").InnerText;
							var positionA3 = xmlDocument.SelectSingleNode("/Position/A3").InnerText;
							var positionA4 = xmlDocument.SelectSingleNode("/Position/A4").InnerText;
							var positionA5 = xmlDocument.SelectSingleNode("/Position/A5").InnerText;
							var positionA6 = xmlDocument.SelectSingleNode("/Position/A6").InnerText;
							var getIdle = xmlDocument.SelectSingleNode("/Position/Idle").InnerText;     //access A1 to A6 and idle status

							idle = getIdle == "0" ? false : true;

							if (idle != beforeIdle)     //idle has been changed
							{
								var statusChangeEventArgs = new StatuChangeEventArgs();
								statusChangeEventArgs.idle = idle;						//access idle
								SatatusChanged?.Invoke(this, statusChangeEventArgs);    //trigger event
								beforeIdle = idle;
							}

							var upDataInEventArgs = new UpDataInEventArgs();
							upDataInEventArgs.A1 = float.Parse(positionA1);
							upDataInEventArgs.A2 = float.Parse(positionA2);
							upDataInEventArgs.A3 = float.Parse(positionA3);
							upDataInEventArgs.A4 = float.Parse(positionA4);
							upDataInEventArgs.A5 = float.Parse(positionA5);
							upDataInEventArgs.A6 = float.Parse(positionA6);				//access A1 to A6
							UpDataIn?.Invoke(this, upDataInEventArgs);					//trigger event

							SpinWait.SpinUntil(() => { return false; }, 10);    //wait 0.001 second
						}
					}
				}
				catch (Exception ex)        // try has error
				{
					Console.WriteLine(ex.ToString());       //write error
					break;
				}
			}
		}

		public void Stop()
		{
			if (myClient != null)
			{
				myClient.Close();       
				myClient = null;
			}
		}
	}
}
  ```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwOTQwNDA5NjYsMTEzMjM1NjkzOCwtMj
g3MDMwNzIxXX0=
-->