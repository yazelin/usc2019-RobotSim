## 五、自動化專案實作 一
### KUKA Srver端通訊程式 EKI基礎
1.網路通訊手臂EKI
  - EKI [參考文件](http://www.wtech.com.tw/public/download/manual/kuka/krc4/KST-Ethernet-KRL-21-En.pdf)
  - 下載xml檔案:[https://github.com/yazelin/usc2019-RobotSim/raw/masteㄙr/src/XmlServer.zip](https://github.com/yazelin/usc2019-RobotSim/raw/master/src/XmlServer.zip)
  - Server設定
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
		   <ELEMENT Tag="Data/Direction" Type="INT" Set_Flag="2"/>
		</XML>
	</RECEIVE>
	<SEND>
		<XML>
		</XML>
	</SEND>
</ETHERNETKRL>
  ```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIyMzk1OTE0MywtMjAyNjczODI5NCwxNz
Q2NjQwMTYzLDE3NDk2NjcxMDcsMTgxMTE2NTU5Ml19
-->