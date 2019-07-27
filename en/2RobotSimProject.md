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

	//declare ready object: readyGet
	public Transform readyGet;
	//declare holding object: holdingObject
	public Transform holdingObject;

	//declare Lock() as catching command, and set readyGet's Parent as Gripper
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

	//declare LockReadyGet() for catching a ready object
	public void LockReadyGet()
	{
		Lock(readyGet);
	}
	//declare UnlockToWorld() to unlock the holding object
	public void UnlockToWorld()
	{
		if (holdingObject)
		{
			holdingObject.parent = null;
		}
		holdingObject = null;//put the holding object to World Root
	}
	//declare OnTriggerEnter for detecting object ready for gripping
	void OnTriggerEnter(Collider other)
	{
		readyGet = other.transform;
	}
	//declare OnTriggerExit
	void OnTriggerExit(Collider other)
	{
		if (readyGet == other.transform)
		{
			readyGet = null;
		}
	}
}

```
- Add GripperCommand

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
			//gripping
			gripper.LockReadyGet();
			//play gripping animation
			if (animatorGripper)
			{
				animatorGripper.speed = 1;
				animatorGripper.Play("Lock", -1, 0);
			}
		}
		else
		{
			//unlock gripper
			gripper.UnlockToWorld();
			//play un-lock animation
			if (animatorGripper)
			{
				animatorGripper.speed = 1;
				animatorGripper.Play("UnLock", -1, 0);
			}
		}

		return (line + 1);
	}

	public override string ExportDat()
	{
		//return nothing to Dat file
		return "";
	}

	public override string ExportSrc()
	{
		//return  GripperLock(true/false) to src file
		return tab + "GripperLock(" + Lock.ToString() + ");" + Environment.NewLine;
	}

	public override string UpdateName()
	{
		//rename Gameobject
		return (gameObject.name = "GripperLock(" + Lock.ToString() + ")");
	}

}
```
- adjust gripper reaching range to detect object for gripping

![Image](../img/AddGripper_3.png)
- Add object

![Image](../img/AddSphereGameobject.png)
- Add gripping func to gripperscript 

![Image](../img/AddGripperScript.png)
- Add Empty GameObject and then add GripperCommand

![Image](../img/AddGripperCommandScript_1.png)
![Image](../img/AddGripperCommandScript_2.png)

- Test

![Image](../img/GripperTest.gif)
- Repeat 

![Image](../img/GripperTest2.gif)



- what else RobotSim can do?
  - [RobotSim forum](http://forum.wtech.com.tw/viewforum.php?f=17&sid=4a42cdd8643e5518dd23f732ca23f0c4).
  
### RobotSim export and import to WorkVisual Project
- WorkVisual project

![Image](../img/WorkVisualWindow.png)
- RobotSim export code

![Image](../img/ExportProgram1.png)
![Image](../img/ExportProgram2.png)
- WorkVisual import 

![Image](../img/ImportProgram1.png)
![Image](../img/ImportProgram2.png)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU5MzcyOTM1MSwyMDc3ODA1MjgzLDE5OT
UyOTE0MzIsMTczOTk0NDkxOCwtOTAyMjY5OTUxLDQ0Mzg1MTI1
LC00MDIyODI2MDYsMTA0MzYyNTAyOSwzNTA2ODkyOCwtMTk1Mj
Y0MzkxNSwxNzg0NTcwNDYsMjEzNzcyNzU2OCw3NzQ4NDE3MzEs
LTE5Njg2OTk3MjQsNjQ1MDY2ODM2LC0xMjMxNDU1MTMsMTg0ND
AzNDg2Niw5ODkyMjk3MDMsLTY1MDEwODM0NiwtMzk4OTYzMDcz
XX0=
-->