## 二、RobotSim專案製作

### RobotSim完整專案
- 顯示訊息功能

<iframe width="560" height="315" src="https://www.youtube.com/embed/e1HLzD1LAZ4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

RobotCommandMessage.cs 程式碼 
```cs
//RobotCommandMessage.cs
using RobotSim;
using UnityEngine;
using System;

public class RobotCommandMessage : RobotCommand
{
	//顯示的訊息
	public string Message = string.Empty;
	
	//檢查是否未設定訊息
	public override bool Check()
	{
		if (Message == string.Empty)
		{
			errorMassage = "未填入訊息";
			return false;
		}
		else
		{
			return true;
		}
	}

	public override int Execute()
	{
		//使用DebugConsole印出所設定的息
		Debug.Log(Message);
		//動作完成，執行下一行
		return (line + 1);
	}

	public override string ExportDat()
	{
		//不需要輸出任何內容到手臂程式的Dat檔中
		return string.Empty;
	}

	public override string ExportSrc()
	{
		//輸出 MsgNotify("訊息內容")  到手臂程式src檔內
		return tab + "MsgNotify(\"" + Message + "\")" + Environment.NewLine;
	}

	public override string UpdateName()
	{
		////更新Gameobject在階層視窗內的名稱
		return (gameObject.name = "MsgNotify(\"" + Message + "\")");
	}
}
```

- RobotSim程式設計擴充 夾娃娃機
  - 視實際進度彈性調整 [參考教學](https://yazelin.github.io/cnu2018-RobotSim/)

- 在RobotSim 中還能做什麼?
  - [歡迎加入RobotSim討論區](http://forum.wtech.com.tw/viewforum.php?f=17&sid=4a42cdd8643e5518dd23f732ca23f0c4).
  
### RobotSim匯出 並匯入WorkVisual專案
- WorkVisual 環境

![Image](./img/WorkVisualWindow.png)
- RobotSim 匯出程式

![Image](./img/ExportProgram1.png)
![Image](./img/ExportProgram2.png)
- WorkVisual 匯入程式

![Image](./img/ImportProgram1.png)
![Image](./img/ImportProgram2.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY1MDEwODM0NiwtMzk4OTYzMDczLDExNz
M1OTk4NjYsLTQxNjE2OTY2NywtNTcwODMyNjUxLDE0MDI0MTQx
NTVdfQ==
-->