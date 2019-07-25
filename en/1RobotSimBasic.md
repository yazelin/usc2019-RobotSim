## 一、Basic operation

## Industrial Robot Introduction

### 6-axis Robots
![Image](../img/RobotSystem.jpg)

### Axis
- A1~A6 

![Image](../img/RobotAxis.jpg)

### Space
- Base Space

![Image](../img/RobotCoordinateSystem.jpg)

- Tool Space

![Image](../img/Tool.jpg) 

### The basic concepts of robotics lon-line earning 
- Embeded RobotSim simulation on WebPlaer
-   [RobotSim WebPlayer](http://www.wtech.com.tw/robotsim)
- The basic concepts of robotics includes
	- Coordinate systems
		- WORLD
		- BASE
		- TOOL    
	- Jogging Mode
		- Cartesian jogging with XYZ ABC according to the selected coordinate system
		- Axis-specific jogging
	- Motion type
		- PTP
		- LIN
		- CIRC
	- Axis Range Limitation
		- A1~A6
	- Teaching and Programing
		- Teach several points to make a robot motion path. 
		- Repeat  the path by 

## RobotSim環境及基本操作

### RobotSim 下載-安裝-試用
<iframe width="560" height="315" src="https://www.youtube.com/embed/xv4v_fOwAC0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- 下載頁面 [連結](http://www.wtech.com.tw/download)
- 影片參考 [連結](https://www.youtube.com/watch?v=xv4v_fOwAC0&index=20&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

### RobotSim 教點-程式-模擬
<iframe width="560" height="315" src="https://www.youtube.com/embed/4Gk7K88B10c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- 影片參考 [連結](https://www.youtube.com/watch?v=4Gk7K88B10c&index=21&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

### RobotSim 設定Tool-更新點位-模擬動作
<iframe width="560" height="315" src="https://www.youtube.com/embed/NLA6A_qWDgs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- 影片參考 [連結](https://www.youtube.com/watch?v=NLA6A_qWDgs&index=22&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

### RobotSim 設定Base-設定手臂-匯出程式
<iframe width="560" height="315" src="https://www.youtube.com/embed/izkk5MW-FeY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- 影片參考 [連結](https://www.youtube.com/watch?v=izkk5MW-FeY&index=23&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

## RobotSim程式設計
- 變數 Value
  - Bool、Int、Float、String
  - Set、Add、Sub、Mut、Div

![Image](../img/Value.png) 
- 動作 Motion
  - Base、Tool、Speed
  - PTP 、LIN、CIRC

![Image](../img/Motion.png) 
- 流程控制 Flow
  - Loop、For-Loop、Wait Time
  - If-Else、While、Switch-Case

![Image](../img/Flow.png)

## 練習
- 匯入RobotSim [下載頁面](http://www.wtech.com.tw/download)
- 開啟Robot視窗、Program視窗、Controller視窗
- 加入空場景

![Image](../img/EmptyRobotSimScene.png)
- 加入機器手臂 Robot

![Image](../img/AddRobot.png)
- 加入手臂程式 Program

![Image](../img/AddProgram.png)
- 加入控制器 Controller

![Image](../img/AddController.png)
- 連結Robot、Controller、Program

![Image](../img/LinkProgramRobot.png)
- 設定主攝影機視角

![Image](../img/MainCamera.png)
- 控制手臂加入點位1、點位2

![Image](../img/AddPoint.png)
- 動作指令 PTP、LIN

![Image](../img/AddPTP.png)
![Image](../img/AddP1.png)
- 變數 INT I、流程控制 FOR-LOOP 迴圈

![Image](../img/AddINTI.png)
![Image](../img/AddFORLOOP.png)
- 設定速度 SPEED、WAIT SEC 指令

![Image](../img/AddSPEED.png)
![Image](../img/AddWAITSEC.png)

## 成果
![Image](../img/Week1Program.png)
![Image](../img/Week1DEMO.gif)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYyNjk5NDA1NiwxMDAxODg2MzQ3LDM2Nz
gwNTU4OCwtNTQ3NTY2MzQ0LDUwNzY3NjAwOSwtMTEzMjcxMDk2
LDMwNDQ4MTQxMSw2NTI4ODc4MzIsODIzNTQ3NzM4LC0xNDkxNj
EzNTY1LDEwMzI1Nzk1MzksMTgwOTQ4Mzc3LC0xMzI4NTI2NTk4
LC0xNzc3MTk3Nzk0LC0xODgyMjY5NTUyLDg0MDA1ODk5LC0xNT
M1NDk1NjY1LC0yMDE5MzUzNTU0LC0xMzcxMTY1MDE4LDE5Nzc3
Njk0NTZdfQ==
-->