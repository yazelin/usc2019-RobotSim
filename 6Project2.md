## 六、自動化專案實作 二
### KUKA Srver端通訊程式

1.建立專案資料夾、加入框架程式
- 建立ClawMachine資料夾
	- 加入Main程式、Core資料夾
- Core資料夾
	- 加入Core、Server程式，Action、Motion資料夾
- Action資料夾
	- 加入Action程式

2.撰寫框架Server程式
  - 定義中斷條件，確認手臂是否有收到資料
  
 ```
GLOBAL DEF Server()  
   
   ;定義Flag[2]=true 中斷所有動作 執行Data_In
   GLOBAL INTERRUPT DECL 101 WHEN $FLAG[2]==TRUE DO Data_In()
   $FLAG[2] = FALSE  			;初始化
   INTERRUPT ON 101  			;宣告
  
END
```

- Data_In_CCD( )為判斷接收資料後執行程式

 ```
DEF Data_In()  
   DECL EKI_STATUS RET  
   INT _DIRECTION  
   DECL CHAR EOL[2]  
   CHAR CHANNEL_NAME[24]
  
   _DIRECTION = 0  
   EOL[1] = 13  					;ASCII碼 換行字元
   EOL[2] = 10  
   CHANNEL_NAME[] = SERVER_CONNECTION_LIST[1].NAME[]
  
   RET = EKI_GetInt(CHANNEL_NAME[],"Data/Direction",_DIRECTION)  ;接收資料
  
   RET = EKI_Send(CHANNEL_NAME[], "Comfirm") 			;傳送確認字串
   RET = EKI_Send(CHANNEL_NAME[], EOL[])  			;傳送換行字元
  
   IF Action_Get_Idle() THEN  					;Idle為閒置狀態
      Action_Set_Command_Info(_DIRECTION)  			;將收到資料傳至Info
      Action_Set_Command_Type(#COMMAND_DECIDE)  		;將Action Type改為判斷
      Server_Set_Ready(TRUE)  					;Server確認收到資料 可執行
   ENDIF  
  
   $FLAG[2] = FALSE  						;初始化Flag[2]
END
```

- 加入回傳訊息程式，告訴 PC 已完成動作

 ```
GLOBAL DEF Send()  
   DECL EKI_STATUS RET  
   DECL CHAR EOL[2]  
   CHAR CHANNEL_NAME[24]
   
   EOL[1] = 13  
   EOL[2] = 10  
   CHANNEL_NAME[] = SERVER_CONNECTION_LIST[1].NAME[]

   RET = EKI_Send(CHANNEL_NAME[], "Finish")  		;傳送結束字串
   RET = EKI_Send(CHANNEL_NAME[], EOL[])  		;傳送換行字元
END
```

- 定義Server.dat檔
	- SERVER_CONNECTION_LIST[1].NAME[ ] 設定為 "XmlServer"

3.在Core需初始化及判斷條件進入Action
- Core初始化

 ```
GLOBAL DEF Core ()  
   BAS(#BASE, 0)  		;設定base
   BAS(#TOOL, 1)  		;設定tool
  

   IOControl()  		;IO初始化
   Exception()  		;事件初始化
  
   Server_Set_Ready(FALSE)		;Server初始化  
   Server()  				;定義中斷
   Server_Start(1)  			;開啟Server
END
```

- Core_Run判斷進入Action條件

 ```
GLOBAL DEF Core_Run()  
  
   PTP XHOME  		;home點
  
   REPEAT  
  
   WHILE ( ( NOT Event() ) AND ( NOT Error() ) )  
  
   IF Server_Get_Ready() THEN  		;判斷Ready
      Action()  
   ENDIF  
  
   ENDWHILE  
  
   WHILE Event()  
   ENDWHILE  
  
   WHILE Error()  
   ENDWHILE  
   UNTIL SYS_EXIT  
END
```

4.Action判斷條件
- 需再Action.dat檔內加入宣告
	- GLOBAL ENUM COMMAND_DECIDE
	- INT _DIRECTION



5.Motion執行動作
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MzgyMDM0MjUsLTQwNTE5NzAxMywtNT
c0ODYxNDQ0LDc2NDQ0MzYzNywzMzg2NTAyODMsMTQyMDM0MDk2
MywxMjQzMDMyNjgyLC0xMDUwMTAwMTUzLC05MDEyODA4MjcsMT
k3NjkzMTkyOCwtMjAzMzc0Nzc0NywtMTk4MTQ5ODk5NV19
-->