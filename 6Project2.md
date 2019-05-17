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
   $FLAG[2] = FALSE  ;初始化
   INTERRUPT ON 101  ;宣告
  
END
```
- Data_In_CCD( )為判斷接收資料後執行程式
 ```
DEF Data_In()  
   DECL EKI_STATUS RET  
   INT _DIRECTION  
   DECL CHAR EOL[2]  
  
   _DIRECTION = 0  
   EOL[1] = 13  		;ASCII碼 換行字元
   EOL[2] = 10  
  
   RET = EKI_GetInt("XmlServer","Data/Direction",_DIRECTION)  ;接收資料
  
   RET = EKI_Send("XmlServer", "Comfirm")  ;傳送確認字串
   RET = EKI_Send("XmlServer", EOL[])  ;傳送換行字元
  
   IF Action_Get_Idle() THEN  ;Idle為閒置狀態
      Action_Set_Command_Info(_DIRECTION)  ;將收到資料傳至Info
      Action_Set_Command_Type(#COMMAND_DECIDE)  ;將Action Type改為判斷
      Server_Set_Ready(TRUE)  ;卻ㄖ
   ENDIF  
  
   $FLAG[2] = FALSE  
END
```
- 加入回傳訊息程式，告訴 PC 已完成動作
 ```
GLOBAL DEF Send()  
   DECL EKI_STATUS RET  
   DECL CHAR EOL[2]  
   EOL[1] = 13  
   EOL[2] = 10  

   RET = EKI_Send("XmlServer", "Finish")  
   RET = EKI_Send("XmlServer", EOL[])  
END
```
3.在Core需初始化、Core需判斷Ready

4.Action判斷條件

5.Motion執行動作
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTc5MTk3MTMsLTEwNTAxMDAxNTMsLT
kwMTI4MDgyNywxOTc2OTMxOTI4LC0yMDMzNzQ3NzQ3LC0xOTgx
NDk4OTk1XX0=
-->