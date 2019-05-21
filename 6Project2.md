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
  
```sh
GLOBAL DEF Server()  
   
   ;定義Flag[2]=true 中斷所有動作 執行Data_In
   GLOBAL INTERRUPT DECL 101 WHEN $FLAG[2]==TRUE DO Data_In()
   $FLAG[2] = FALSE  			;初始化
   INTERRUPT ON 101  			;宣告
  
END
```

- Data_In_CCD( )為判斷接收資料後執行程式

```sh
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

```sh
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

```sh
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

```sh
GLOBAL DEF Core_Run()  
  
   PTP XHOME  		;home點
  
   REPEAT  
  
   WHILE ( ( NOT Event() ) AND ( NOT Error() ) )  
  
   IF Server_Get_Ready() THEN  		;判斷Ready
      Action()  
   ENDIF  
  
   ENDWHILE  
   
   UNTIL SYS_EXIT  
END
```

4.Action判斷條件
- 需再Action.dat檔內加入宣告

```sh
 GLOBAL ENUM ACTION_COMMAND_TYPE COMMAND_DECIDE
 GLOBAL STRUC ACTION_INFO_STRUC INT _DIRECTION
 DECL ACTION_INFO_STRUC ACTION_INFO 加入 _DIRECTION 0
```

- Action內判斷現在需要執行內容

```cls
GLOBAL DEF Action ( )  
   Action_Before()  		;Action開始前要做的事
  
   SWITCH ACTION_COMMAND.TYPE  		
  
   CASE #COMMAND_DECIDE  		;判斷是移動還是夾
	   Wt_Action_Next(ACTION_INFO)  	
	   RETURN  
   
   CASE #COMMAND_MOV  		;移動
	   Wt_Action_Mov(ACTION_INFO)  
  
   CASE #COMMAND_GETPUT  		;夾
	   Wt_Action_GetPut()  
  
   ENDSWITCH  
  
   Action_After()  		;Action結束後要做的事
END
```

- Action結束後 After需要判斷此次命令動作是否結束

```src
DEF Action_After()  
  
   IF (NOT Event()) AND (NOT Error()) THEN  
      SWITCH ACTION_COMMAND.TYPE  		;如果是移動or夾
         CASE #COMMAND_MOV  
            Server_Set_Ready(FALSE)  		;Ready = FALSE
            Action_Set_Idle(TRUE)  		;Idle改回TRUE
            Send()  				;傳送結束指令
         CASE #COMMAND_GETPUT  
            Server_Set_Ready(FALSE)  
            Action_Set_Idle(TRUE)  			
            Send()  
         DEFAULT  
      ENDSWITCH  
   ENDIF  
END
```

- 讓程式能從外面變更Type、Info

```sh
GLOBAL DEF Action_Set_Command_Type(_COMMAND_TYPE:IN)  
   DECL ACTION_COMMAND_TYPE _COMMAND_TYPE  
  
   ACTION_COMMAND.TYPE = _COMMAND_TYPE  	;下一步改為判斷
END  
  
GLOBAL DEF Action_Set_Command_Info(_TO_INDEX:IN)  
   INT _TO_INDEX  
  
   ACTION_INFO._DIRECTION = _TO_INDEX  		;Server接收到資料存進Info
END
```

5.Motion執行動作

- Motion動作移動

```patch
DEF Wt_Motion_Direction (_DIRECTION:IN)  
   INT _DIRECTION, DISTANCE_ADD, DISTANCE_DEL  
   E6POS POSITION  
  
   DISTANCE_ADD = 100  
   DISTANCE_DEL = -100  
  
   POSITION = {X 0,Y 0,Z 0,A 0,B 0,C 0}  
  
   SWITCH _DIRECTION  
      CASE 1  
         POSITION.X = DISTANCE_ADD  
      CASE 2  
         POSITION.X = DISTANCE_DEL  
      CASE 3  
         POSITION.Y = DISTANCE_ADD  
      CASE 4  
         POSITION.Y = DISTANCE_DEL  
   ENDSWITCH  
  
   LIN_REL POSITION  
  
END
```

- Motion動作夾

```sh
DEF Wt_Motion_GetPut ()  
   INT DISTANCE_ADD, DISTANCE_DEL  
   E6POS POSITION  
  
   DISTANCE_ADD = 100  
   DISTANCE_DEL = -100  
  
   POSITION = {X 0,Y 0,Z 0,A 0,B 0,C 0}  
  
   POSITION.Z = DISTANCE_DEL  
  
   LIN_REL POSITION  
  
   POSITION.Z = DISTANCE_ADD  
  
   LIN_REL POSITION  
END
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMTk3MTUxMjMsOTA4OTcwOTM3LC0xNz
E4MzUyMTM5LDIxMzg5OTAzNzcsLTE5NTk2NDg2MywtMTIyMjAw
NTY4NywtMjEzMTczMTUyNSw1NTI4OTYyNjMsLTIwNzY3Mzc5MT
csMTk3OTE0NzMxMSwtMTEyNDk2Mjg0Niw1ODU1NDc5MTQsMTQ3
MjYyNDMwNiwtMjAyMjU2NjY1OCwtMTE2NzM2MDk5MCwyNTYzMD
A4ODgsNzU3NTExNjY1LC00MDAyMDA0NDQsLTIwNDk5Mjc1MCwt
MTQwNzczNjUwXX0=
-->