## 二、RobotSim專案製作
### [繳交作業](https://drive.google.com/drive/folders/104_rw30SUGLiESvD4R0ukJIDlGs7t98Y?fbclid=IwAR172PehbkoKq6Lboyup1Wp-YAIbEKpJTQUJWJMZ9zZYzy_iTaDapXleThA)
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

- 設定Home點位置

![Image](./img/SetHomePosition_1.png)
![Image](./img/SetHomePosition_2.png)
- 加入夾爪模型(用Sphere代替)

![Image](./img/AddGripper_1.png)
![Image](./img/AddGripper_2.png)
![Image](./img/AddGripper_3.png)
- 加入Gripper程式
```cs
//Gripper.cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Gripper : MonoBehaviour
{
	// Gripper程式 修改物體的Transform.Parent來模擬夾取
	//準備夾取的物件
	public Transform readyGet;
	//目前夾持的物件
	public Transform holdingObject;

	//夾取指令
	public void Lock(Transform product)
	{
		if (holdingObject == null)
		{
			if (product)
			{
				product.transform.parent = transform;
				holdingObject = product;
			}
		}
	}

	//傳回目前所夾持物
	public Transform Unlock()
	{
		Transform returnObject = holdingObject;
		holdingObject = null;//清空目前所持物

		return returnObject;
	}

	//夾取readyGet物件
	public void LockReadyGet()
	{
		Lock(readyGet);
	}
	//放開夾取物件
	public void UnlockToWorld()
	{
		if (holdingObject)
		{
			holdingObject.parent = null;
		}
		holdingObject = null;//把手上拿著的東西丟到世界Root去
	}
	//偵測目前可夾取物
	void OnTriggerEnter(Collider other)
	{
		readyGet = other.transform;
	}
	//移除目前圖夾取物
	void OnTriggerExit(Collider other)
	{
		if (readyGet == other.transform)
		{
			readyGet = null;
		}
	}
}
```
- 加入GripperCommand

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
eyJoaXN0b3J5IjpbMTQ2ODg3MzM3NywtMTIzMTQ1NTEzLDE4ND
QwMzQ4NjYsOTg5MjI5NzAzLC02NTAxMDgzNDYsLTM5ODk2MzA3
MywxMTczNTk5ODY2LC00MTYxNjk2NjcsLTU3MDgzMjY1MSwxND
AyNDE0MTU1XX0=
-->