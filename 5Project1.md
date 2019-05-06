## 五、自動化專案實作 一
### KUKA Srver端通訊程式 EKI基礎

1.網路通訊手臂EKI
  - EKI [參考文件](http://www.wtech.com.tw/public/download/manual/kuka/krc4/KST-Ethernet-KRL-21-En.pdf)(https://github.com/yazelin/usc2019-RobotSim/raw/master/src/XmlServer.zip)
  - Server設定
	  - 在Files中打開Config\User\Commoon\EthernetKRL\XmlServer.xml
	  - ![Image](./img/Demonstration2.PNG)

  ```xml
  <ETHERNETKRL>
	<CONFIGURATION>
		<EXTERNAL>
			<TYPE>Client</TYPE>   ;設定外部為Client
		</EXTERNAL>
		<INTERNAL>
			<IP>192.168.1.147</IP>	;設定連線IP
			<PORT>54600</PORT>		;這定通訊埠
			<ALIVE Set_Flag="1"/>	;當確定連線後Flag[1] = TRUE
		</INTERNAL>
	</CONFIGURATION>
	<RECEIVE>
		<XML>
		   <ELEMENT Tag="Data/Direction" Type="INT" Set_Flag="2"/>	;設定接收到的資料 Tag="路徑" Type="資料型別" 接收資料後Flag[2]=TRUE
		</XML>
	</RECEIVE>
	<SEND>
		<XML>
		</XML>
	</SEND>
</ETHERNETKRL>
  ```

  - 在資料夾中新增程式
	  - 在 KRL\R1\Program\test 資料夾點擊右鍵 選取 Add>Module 加入後命名程式名稱

  - EKI手臂程式
  ```xml
DEF XmlServer( )
   INT i
   DECL EKI_STATUS RET
   INT value
   char EOL[2]
   EOL[1] = 13
   EOL[2] = 10
   
   RET=EKI_Init("XmlServer")
   RET=EKI_Open("XmlServer")
   
   wait for $FLAG[1]
   
   FOR i=(1) TO (20)
      valueChar[i]=0
   ENDFOR
   
   WAIT FOR $FLAG[2] == TRUE
   
   RET=EKI_GetString("XmlServer","Sensor/A",valueChar[])
   
   MsgNotify(valueChar[])
   
   RET = EKI_Send("XmlServer", "Comfirm")
   RET = EKI_Send("XmlServer", EOL[])
   
   wait for $FLAG[1]==FALSE
   
   RET=EKI_Clear("XmlServer")
END
  ```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MjQ4MzgyODgsMTg4MTI3MTQyNSw4Nj
A4NDE5MjMsLTkyODU4NDU4MiwxNjUzMjA2MTE5LC0yMDI2NzM4
Mjk0LDE3NDY2NDAxNjMsMTc0OTY2NzEwNywxODExMTY1NTkyXX
0=
-->