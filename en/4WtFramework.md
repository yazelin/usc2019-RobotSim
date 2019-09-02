## 四、WtFramework 開發框架

### Winform Client 端通訊程式

1. 安裝
  - 於 WorkVisual 內點選 File/Cataloghandling...
  - 於 Catalogs 視窗點選 KRL Templates 後按 > 按鈕 加入功能
  - ![Image](../img/AddKRLTemplates.png)
  - 將 WtFramework.zip 解壓縮後將 KUKA Templates資料夾 覆蓋 C:\Users\User\Documents\KUKA Templates 資料夾
2. 網路通訊
  - 下載xml檔案:[https://github.com/yazelin/usc2019-RobotSim/raw/master/src/XmlServer.zip](https://github.com/yazelin/usc2019-RobotSim/raw/master/src/XmlServer.zip)
  - 在 EthernetKRL 點右鍵選擇 Add external file 加入 Xml.Servver.xml
  - ![Image](../img/Demonstration.PNG)
  - 點選XmlServer.Xml
  - ![Image](../img/Demonstration2.PNG)
  - Server設定
  
```xml
<ETHERNETKRL>
   <CONFIGURATION>
      <EXTERNAL>
         <TYPE>Client</TYPE>
      </EXTERNAL>
      <INTERNAL>
         <IP>192.168.1.147</IP>			;設定手臂IP
         <PORT>54600</PORT>				;設定連線port
         <ALIVE Set_Flag="1"/>			;當確定連線後Flag[1] = TRUE
      </INTERNAL>
   </CONFIGURATION>
   <RECEIVE>
      <XML>
         <ELEMENT Tag="Data/Direction" Type="INT" Set_Flag="2"/>   ;設定接收到的資料 Tag="路徑" Type="資料型別" 接收資料後Flag[2]=TRUE
      </XML>
   </RECEIVE>
   <SEND>
      <XML>
         <ELEMENT Tag="Result/Answer" Type="STRING"/>  ;設定輸出資料
      </XML>
   </SEND>
</ETHERNETKRL>
   ```

3. 夾娃娃機PC端操作介面
- 步驟
	1. 介面設計
	2. 開啟關閉功能
	3. 建立按鈕傳送訊息
	4. 註冊Click事件
	5. 傳送接收
	6. 測試及改寫

<iframe width="560" height="315" src="https://www.youtube.com/embed/DQzu3EQPiYw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

  - Winform 介面設計
  - ![Image](../img/WinFormInterface.PNG)
  
  <iframe width="560" height="315" src="https://www.youtube.com/embed/whyCVhJ1Opo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
  
  - Client 啟動及關閉按鍵 Form1
  
  ```cs
 		Client client = new Client();
		private void buttonStart_Click(object sender, EventArgs e)
		{
			client.Start("127.0.0.1", 54600);
		}

		private void buttonStop_Click(object sender, EventArgs e)
		{
			client.Stop();
		}
```
  
  - Client 啟動及關閉程式 Client
  
  ```cs
	class Client
	{
		TcpClient myClient;         //建立TcpClient

		public Client() { }


		public void Start(string ip, int port)
		{
			if (myClient != null)                   //myClient有被new出來的話 結束
			{
				return;
			}
			myClient = new TcpClient(ip, port);     //設定Ip跟Port
			Task.Run(() => ClientService());        //在另一個執行續中執行  ClientService()  ; 由電腦決定是否產生新執行續
		}

		public void Stop()
		{
			if (myClient != null)
			{
				myClient.Close();       //關閉Client
				myClient = null;
			}
		}
	}
```

<iframe width="560" height="315" src="https://www.youtube.com/embed/shkiS5mD5nw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

  - 建立各項按鈕需傳入資料 Form1
  
  ```cs
		private void SetData(string command)
		{
			client.Send(command);
		}

		private void buttonFront_Click(object sender, EventArgs e)
		{
			SetData("1");
		}

		private void buttonBack_Click(object sender, EventArgs e)
		{
			SetData("2");
		}
		
		private void buttonLeft_Click(object sender, EventArgs e)
		{
			SetData("3");
		}

		private void buttonRight_Click(object sender, EventArgs e)
		{
			SetData("4");
		}

		private void buttonGet_Click(object sender, EventArgs e)
		{
			SetData("5");
		}
  ```
  
 - 提示-注意
	1.  元件名稱
	2.  註冊事件
<iframe width="560" height="315" src="https://www.youtube.com/embed/GnbQULTbTcM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
	
  - Client端傳送程式 Client
  
  ```cs
  	private string sendData = string.Empty;
		
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

					if (myClient != null)           //myClient有被new出來
					{
						StreamReader streamReader = new StreamReader(myClient.GetStream());     //建立StreamReader
						StreamWriter streamWriter = new StreamWriter(myClient.GetStream());     //建立StreamWriter

						while (myClient.Connected)      //myClient連線
						{
							if (sendData != string.Empty)       //sendData不是空字串
							{
								streamWriter.WriteLine(sendData);       //寫出sendData資料
								streamWriter.Flush();                   //傳送
								Console.WriteLine("Client To Server : " + sendData);

								var data = streamReader.ReadLine();     //讀取Server端傳回資料
								Console.WriteLine("From Server : " + data);

								sendData = string.Empty;
							}
							SpinWait.SpinUntil(() => { return false; }, 10);    //等待0.01秒
						}
					}
				}
				catch (Exception ex)        // 執行try發生錯誤
				{
					Console.WriteLine(ex.ToString());       //印出錯誤訊息
					break;
				}
			}
		}
  ```

<iframe width="560" height="315" src="https://www.youtube.com/embed/MR59pzw0iq8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

  - Server端測試程式:[https://github.com/yazelin/usc2019-RobotSim/raw/master/src/WinFormServerTest.zip](https://github.com/yazelin/usc2019-RobotSim/raw/master/src/WinFormServerTest.zip)
  
  - 改寫傳送資料為XML Form1
```cs
  	private void SetData(string command)
		{
			string dataSend = " ";
			dataSend = "<Data><Direction>"+ buttonNumber +"</Direction></Data>";
			client.Send(dataSend);
		}
  ```
  
  - PC端手臂模擬程式
<iframe width="560" height="315" src="https://www.youtube.com/embed/W62LbDkruTw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
 
  模擬程式下載: [https://github.com/yazelin/usc2019-RobotSim/raw/master/src/Play.zip](https://github.com/yazelin/usc2019-RobotSim/raw/master/src/Play.zip)  
解壓縮後執行 USC2019RobotSim.exe
```
IP 127.0.0.1 
Port 54600
前 <Data><Direction>1</Direction></Data>
後 <Data><Direction>2</Direction></Data>
左 <Data><Direction>3</Direction></Data>
右 <Data><Direction>4</Direction></Data>
夾 <Data><Direction>5</Direction></Data>
  ```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg3NTI3NzM3LDEzNjg2MDE0MjMsLTIwMD
IyNzM1NzMsMTk5OTAzNjA2MSwtMTEzNzIyODE2OSwxMDMxODgz
MDM2LDkxODg4NzU4MCwxMDMxODgzMDM2LC0xMzUxMzYwMTAwLD
ExMzYxMDMxMjcsMTMxMzY1ODQ4NywtMTIwMDEyMjY1LC0xNjg0
MTc0NjM3LC04NDc2MzQxNTMsLTUwMTg2Nzc0OSwxMTk1MzkyNj
czLC0xNjE2NDg2MTQ3LDQ3Nzk1MDA0NCwtMTIxNzMxMDc3OSw1
ODQ2NzUyNzJdfQ==
-->