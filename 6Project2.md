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
   
   ;定義Flag[2]=true 中斷所有動作
   GLOBAL INTERRUPT DECL 101 WHEN $FLAG[2]==TRUE DO Data_In()
   $FLAG[2] = FALSE  ;初始化
   INTERRUPT ON 101  ;宣告
  
END
```
- Data_In_CCD( )為判斷接收資料後執行程式
 ```
DEF Data_In()  
   DECL EKI_STATUS RET  
   CHAR CHANNEL_NAME[24]  
   INT _DIRECTION  
   DECL CHAR EOL[2]  
  
   _DIRECTION = 0  
   EOL[1] = 13  
   EOL[2] = 10  
   CHANNEL_NAME[] = SERVER_CONNECTION_LIST[1].NAME[]  
  
   RET = EKI_GetInt(CHANNEL_NAME[],"Data/Direction",_DIRECTION)  
  
   RET = EKI_Send(CHANNEL_NAME[], "Comfirm")  
   RET = EKI_Send(CHANNEL_NAME[], EOL[])  
  
   IF Action_Get_Idle() THEN  
      Action_Set_Command_Info(_DIRECTION)  
      Action_Set_Command_Type(#COMMAND_DECIDE)  
      Server_Set_Ready(TRUE)  
   ENDIF  
  
   $FLAG[2] = FALSE  
END
```
- 加入回傳訊息程式，告訴 PC 已完成動作
 ```
GLOBAL DEF Send()  
   DECL EKI_STATUS RET  
   CHAR CHANNEL_NAME[24]  
   DECL CHAR EOL[2]  
   EOL[1] = 13  
   EOL[2] = 10  

   CHANNEL_NAME[] = SERVER_CONNECTION_LIST[1].NAME[]  
   RET = EKI_Send(CHANNEL_NAME[], "Finish")  
   RET = EKI_Send(CHANNEL_NAME[], EOL[])  
END
```
3.在Core需初始化、Core需判斷Ready

4.Action判斷條件

5.Motion執行動作
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzOTk5NDYxMTMsLTEwNTAxMDAxNTMsLT
kwMTI4MDgyNywxOTc2OTMxOTI4LC0yMDMzNzQ3NzQ3LC0xOTgx
NDk4OTk1XX0=
-->