## 三、手臂操作訓練及KRL程式語言
### [繳交作業](https://drive.google.com/drive/folders/1Y3z2fzKdRJWUsqoRW0wzBV0vf2mGEnmF?fbclid=IwAR172PehbkoKq6Lboyup1Wp-YAIbEKpJTQUJWJMZ9zZYzy_iTaDapXleThA)
### 手臂安全及基本操作 [參考文件](http://www.wtech.com.tw/public/download/manual/kuka/krc4/KUKA%20KSS%208.3%20for%20End%20User.pdf)
- 安全規定
- 操作教導器SmartPad

### 機器手臂專案
實踐KUKA KR3 [專案檔](./src/USCITC.wvs)

### WorkVisual KRL 程式語言 [參考文件](http://www.wtech.com.tw/public/download/manual/kuka/krc4/KUKA%20KRL-Syntax%208.x.pdf)
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
eyJoaXN0b3J5IjpbMTg0Nzc4MDAxNywxODI3NTA5NzM2LDE0Nz
k4ODMyMDZdfQ==
-->