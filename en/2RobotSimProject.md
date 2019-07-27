## RobotSim Project


- Display message

<iframe width="560" height="315" src="https://www.youtube.com/embed/e1HLzD1LAZ4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

RobotCommandMessage.cs Code
```cs
//RobotCommandMessage.cs
using RobotSim;
using UnityEngine;
using System;

public class RobotCommandMessage : RobotCommand
{
	//display message
	public string Message = string.Empty;
	
	//check message 
	public override bool Check()
	{
		if (Message == string.Empty)
		{
			errorMassage = "message empty";
			return false;
		}
		else
		{
			return true;
		}
	}

	public override int Execute()
	{
		//use DebugConsole to print message
		Debug.Log(Message);
		// go to next line
		return (line + 1);
	}

	public override string ExportDat()
	{
		//no message needed to be sent to robot dat files
		return string.Empty;
	}

	public override string ExportSrc()
	{
		//output MsgNotify("message")  to robot src file
		return tab + "MsgNotify(\"" + Message + "\")" + Environment.NewLine;
	}

	public override string UpdateName()
	{
		////rename Gameobject
		return (gameObject.name = "MsgNotify(\"" + Message + "\")");
	}
}
```

- RobotSim code for clip doll machine
  -  [Reference](https://yazelin.github.io/cnu2018-RobotSim/)

- set Home point

![Image](../img/SetHomePosition_1.png)
![Image](../img/SetHomePosition_2.png)
- Add a gripper (using Spherical ball)

![Image](../img/AddGripper_1.png)
![Image](../img/AddGripper_2.png)
![Image](../img/AddGripper_3.png)
- Add a gripper code

```cs
//Gripper.cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Gripper : MonoBehaviour
{
	// Gripper code has two methods for gripping
	// 1.use OnTriggerEnter to catch objects within a default range，and the parent of the holding object is set up to Gripper
	// 2.use the gripper catching animation to move the gripper, and use Rigidbody function for Clipping

	//declare transform object: ready for catching
	public Transform readyGet;
	//the current holding object
	public Transform holdingObject;

	//declare catching command Lock(set readyGet's Parent as Gripper)
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

	//declare Unlock() to return holding object
	public Transform Unlock()
	{
		Transform returnObject = holdingObject;
		holdingObject = null;//clear holding object

		return returnObject;
	}

	//declare LockReadyGet for catching a ready object
	public void LockReadyGet()
	{
		Lock(readyGet);
	}
	//declare UnlockToWorld() 放開夾取物件
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
- 加入GripperCommand(實踐課程試用版 Trial_0_1_6991 內已包含)

```
//RobotCommandGripper.cs
using UnityEngine;
using RobotSim;
using System;

public class RobotCommandGripper : RobotCommand
{
	//declare Gripper object: gripper
	public Gripper gripper;
	//Gripper animator
	public Animator animatorGripper;
	//declare boolen Lock and set as false
	public bool Lock = false;

	// Check()
	public override bool Check()
	{
		if (gripper)
		{
			return true;
		}
		else
		{
			errorMassage = "Gripper is NULL";
			return false;
		}
	}

	//Execute
	public override int Execute()
	{
		if (Lock)
		{
			//夾取(以設定Parent方式)
			gripper.LockReadyGet();
			//夾取(播放動畫)
			if (animatorGripper)
			{
				animatorGripper.speed = 1;
				animatorGripper.Play("Lock", -1, 0);
			}
		}
		else
		{
			//放開(以設定parent方式)
			gripper.UnlockToWorld();
			//放開(播放動畫)
			if (animatorGripper)
			{
				animatorGripper.speed = 1;
				animatorGripper.Play("UnLock", -1, 0);
			}
		}
		//動作完成，執行下一行
		return (line + 1);
	}

	public override string ExportDat()
	{
		//不需要輸出任何程式到Dat檔
		return "";
	}

	public override string ExportSrc()
	{
		//輸出  GripperLock(true/false);  至 手臂程式src檔內
		return tab + "GripperLock(" + Lock.ToString() + ");" + Environment.NewLine;
	}

	public override string UpdateName()
	{
		//更新Gameobject在階層視窗內的名稱
		return (gameObject.name = "GripperLock(" + Lock.ToString() + ")");
	}

}
```
- 調整夾爪碰撞範圍(用來偵測範圍內是否有物體可以夾)

![Image](../img/AddGripper_3.png)
- 加入物體

![Image](../img/AddSphereGameobject.png)
- 夾爪加入Gripper功能

![Image](../img/AddGripperScript.png)
- Program中加入Empty GameObject後加入GripperCommand功能

![Image](../img/AddGripperCommandScript_1.png)
![Image](../img/AddGripperCommandScript_2.png)

- 測試

![Image](../img/GripperTest.gif)
- 來回夾放測試

![Image](../img/GripperTest2.gif)



- 在RobotSim 中還能做什麼?
  - [歡迎加入RobotSim討論區](http://forum.wtech.com.tw/viewforum.php?f=17&sid=4a42cdd8643e5518dd23f732ca23f0c4).
  
### RobotSim匯出 並匯入WorkVisual專案
- WorkVisual 環境

![Image](../img/WorkVisualWindow.png)
- RobotSim 匯出程式

![Image](../img/ExportProgram1.png)
![Image](../img/ExportProgram2.png)
- WorkVisual 匯入程式

![Image](../img/ImportProgram1.png)
![Image](../img/ImportProgram2.png)


<!--stackedit_data:
eyJoaXN0b3J5IjpbOTY3NjUzMzM0LDE5OTUyOTE0MzIsMTczOT
k0NDkxOCwtOTAyMjY5OTUxLDQ0Mzg1MTI1LC00MDIyODI2MDYs
MTA0MzYyNTAyOSwzNTA2ODkyOCwtMTk1MjY0MzkxNSwxNzg0NT
cwNDYsMjEzNzcyNzU2OCw3NzQ4NDE3MzEsLTE5Njg2OTk3MjQs
NjQ1MDY2ODM2LC0xMjMxNDU1MTMsMTg0NDAzNDg2Niw5ODkyMj
k3MDMsLTY1MDEwODM0NiwtMzk4OTYzMDczLDExNzM1OTk4NjZd
fQ==
-->