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
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDk3NTY0MzA2LDExMzIzNTY5MzgsLTI4Nz
AzMDcyMV19
-->