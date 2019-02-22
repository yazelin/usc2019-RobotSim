# 機器手臂程式設計

課程規劃以實際專案進行的順序擬定大綱。
並依大綱依序學習必要技能。
1. 前期規劃
  - 了解現況
  - 如何以自動化替代人力
  - 初步構想
2. 初步模擬 一、二
  - 流程
  - 空間配置(干涉)
3. 實機測試 三、四
  - 硬體安裝、微調
  - 軟體測試、重構
4. 建置完整系統 五、六
  - 周邊設備整合
  - 整合測試
  - 驗收

## 一、課程大綱

### 一、課程大綱(3/13)
1. 課程大綱
2. 手臂基本介紹
3. RobotSim環境及基本操作
  - 下載-安裝-試用 [參考影片](https://www.youtube.com/watch?v=xv4v_fOwAC0&index=20&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo)
  - 教點-程式-模擬 [參考影片](https://www.youtube.com/watch?v=4Gk7K88B10c&index=21&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo)
  - 設定Tool-更新點位-模擬動作 [參考影片](https://www.youtube.com/watch?v=NLA6A_qWDgs&index=22&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo)
  - 設定Base-設定手臂-匯出程式 [參考影片](https://www.youtube.com/watch?v=izkk5MW-FeY&index=23&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo)
4. RobotSim基礎程式
  - 變數
  - 設定
  - 動作
  - 流程控制

### 二、RobotSim專案制作(3/27)
1. RobotSim完整專案
  - RobotSim程式設計擴充 C# [參考](https://yazelin.github.io/cnu2018-RobotSim/)
  - 自訂函式/修改功能
2. RobotSim匯出 並匯入WorkVisual專案

### 三、手臂操作訓練及KRL程式語言(4/10)
1. 手臂安全及基本操作
2. WorkVisual KRL 程式語言
  - 變數
  - 常用函式
  - 動作指令
  - 流程控制

### 四、WtFramework 開發框架(4/24)
1. WtFramework開發框架介紹
  - Core
  - Action
2. 安裝
3. 網路通訊 EKI
  - Server
4. 練習

### 五、自動化專案實作 一(5/08)
1. WtFramework 自動化專案 實作
  - PC端 為主控端 C#
  - Robot端 為被控設備 KRL

### 六、自動化專案實作 二(5/22)
1. WtFramework 自動化專案 實作
  - PC端 為主控端 C#
  - Robot端 為被控設備 KRL


## 手臂基本介紹
### 六軸機器手臂
![Image](./img/RobotSystem.jpg)

### 軸向
- A1~A6 

![Image](./img/RobotAxis.jpg)

### 空間
- Base空間

![Image](./img/RobotCoordinateSystem.jpg)

- Tool空間

![Image](./img/Tool.jpg) 

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
- 影片參考  [連結](https://www.youtube.com/watch?v=xv4v_fOwAC0&index=20&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

### RobotSim 教點-程式-模擬
- 影片參考  [連結](https://www.youtube.com/watch?v=4Gk7K88B10c&index=21&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

### RobotSim 設定Tool-更新點位-模擬動作
- 影片參考  [連結](https://www.youtube.com/watch?v=NLA6A_qWDgs&index=22&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

### RobotSim 設定Base-設定手臂-匯出程式
- 影片參考  [連結](https://www.youtube.com/watch?v=izkk5MW-FeY&index=23&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

## RobotSim程式設計
- 變數 Value
  - Bool、Int、Float、String
  - Set、Add、Sub、Mut、Div
- 動作 Motion
  - Base、Tool、Speed
  - PTP 、LIN、CIRC
- 流程控制 Flow
  - Loop、For-Loop、Wait Time
  - If-Else、While、Switch-Case

## 二、RobotSim專案製作

### RobotSim完整專案
- RobotSim程式設計擴充 (視實際進度彈性調整)
- 自訂函式/修改功能
- 在RobotSim 中還能做什麼?
- [歡迎加入RobotSim討論區](http://forum.wtech.com.tw/viewforum.php?f=17&sid=4a42cdd8643e5518dd23f732ca23f0c4).
  
### RobotSim匯出 並匯入WorkVisual專案
- WorkVisual 環境
- RobotSim匯出程式
- WorkVisual匯入程式
   
## 三、手臂操作訓練及KRL程式語言
### 手臂安全及基本操作
- 安全規定
- 操作教導器SmartPad

### WorkVisual KRL 程式語言
- 變數
  - BOOL
  - INT
  - CHAR
  - CHAR[  ]
- 常用函式
  - BAS(#BASE, REAL_PAR)  
  - BAS(#TOOL, REAL_PAR)
  - BAS(#VEL_CP, REAL_PAR)
  - BAS(#VEL_PTP, REAL_PAR)
  - MsgNotify("this is a notify message")
- 動作指令
  - PTP
  - LIN
  - CIRC
- 流程控制
  - IF-ELSE
  - FOR
  - WHILE
  - REPEAT
  - SWICTH-CASE


## 四、WtFramework 開發框架
- WtFramework開發框架介紹
  - Core
  - Action
- 安裝
- 網路通訊 EKI
- 練習

視實際進度彈性調整

## 五、自動化專案實作 一
- PC端 為主控端
- Robot端 為被控設備

視實際進度彈性調整

## 六、自動化專案實作 二
- PC端 為主控端
- Robot端 為被控設備

視實際進度彈性調整

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA1MTQ3OTM4NSwtMjEwNjE0NjU5MSwxOD
MzMjYyODM4LC0yMTA2MTQ2NTkxLC0xNTEzNTc3NDYwLDMwMDI4
ODkwNSwtMTU3MTc2MTI2MywxMTEyMTMzODk5LC02NjY0MjQ2Mj
QsLTEwOTU1MDQwNzAsMzU0OTUzODQ5LDEwNDYwNDUwOTUsODk2
MDI2ODMxLDcyNjE5OTI2NSwtMTQxNzE2NDU3MSwxNDU0NzE3OD
Y1LDE0NzU4MjUyODUsMTYyODQ5NDIwMyw1NzYzNzUyNzIsMTYy
ODQ5NDIwM119
-->