## 一、RobotSim基礎

## 手臂基本介紹
### 六軸機器手臂
![Image](../img/RobotSystem.jpg)

### 軸向
- A1~A6 

![Image](../img/RobotAxis.jpg)

### 空間
- Base空間

![Image](../img/RobotCoordinateSystem.jpg)

- Tool空間

![Image](../img/Tool.jpg) 

### 線上模擬環境
- 我們把模擬環境放在網站上了
- 網址在這邊  [RobotSim WebPlayer](http://www.wtech.com.tw/robotsim)
- 在模擬器中我們可以學到這些
	- 座標系
		- WORLD
		- BASE
		- TOOL    
	- 操作方式
		- XYZ ABC
		- AXIS
	- 運動指令
		- PTP
		- LIN
		- CIRC(網頁版的模擬器中沒有) 
	- 軸極限  
		- A1~A6
	- 手臂程式執行方式
		- 先教點
		- 用指令讓手臂重現動作 

## RobotSim環境及基本操作

### RobotSim 下載-安裝-試用
<iframe width="560" height="315" src="https://www.youtube.com/embed/xv4v_fOwAC0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- 下載頁面 [連結](http://www.wtech.com.tw/)
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
- 匯入RobotSim [下載頁面](http://www.wtech.com.tw/robotsim)
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
eyJoaXN0b3J5IjpbMTgxOTM2Njg5NSwxNzgxOTEyNCwxMDMyNT
c5NTM5LDE4MDk0ODM3NywtMTMyODUyNjU5OCwtMTc3NzE5Nzc5
NCwtMTg4MjI2OTU1Miw4NDAwNTg5OSwtMTUzNTQ5NTY2NSwtMj
AxOTM1MzU1NCwtMTM3MTE2NTAxOCwxOTc3NzY5NDU2LDQyMzM5
MzAxNSwzNjI3NzE1MjMsMTEzMTQzMDA5OSwyNjgxNzcwMDQsLT
MzNzM5MjEwNSwtNjUwMzI3MTU1LC02MDI5Njg5NzAsLTEwNTQz
MTI4ODBdfQ==
-->