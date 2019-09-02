## 三、手臂操作訓練及KRL程式語言
### [繳交作業](https://drive.google.com/drive/folders/1Y3z2fzKdRJWUsqoRW0wzBV0vf2mGEnmF?fbclid=IwAR172PehbkoKq6Lboyup1Wp-YAIbEKpJTQUJWJMZ9zZYzy_iTaDapXleThA)

- 安全規定    [手臂安全](http://www.wtech.com.tw/public/download/manual/%E6%A9%9F%E6%A2%B0%E6%89%8B%E8%87%82%E5%AE%89%E5%85%A8%E6%AA%A2%E6%9F%A5%E8%A1%A8.pdf)
- 操作教導器SmartPad

### 機器手臂操作
<iframe width="560" height="315" src="https://www.youtube.com/embed/3UZCKB1lnW4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

影片中解釋錯誤的部份： 
- 不是把電腦的IP改成跟手臂的一樣
- 而是將電腦的IP設成和手臂相同網段不能一樣

### 機器手臂專案
實踐KUKA KR3 [專案檔](https://github.com/yazelin/usc2019-RobotSim/raw/master/src/USCITC.wvs)

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

### 實機測試


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwOTA1NTY0ODgsLTEwMDYyNDM4NywxMz
E1NDI3MzY2LC0xNjAzNjYzNzcxLC0yMTA4NjY3MzY3LDE4NDc3
ODAwMTcsMTgyNzUwOTczNiwxNDc5ODgzMjA2XX0=
-->