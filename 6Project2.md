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
GLOBAL INTERRUPT DECL 102 WHEN $FLAG[2]==TRUE DO Data_In()

$FLAG[2] = FALSE

INTERRUPT ON 102
```

3.在Core需初始化、Core需判斷Ready

4.Action判斷條件

5.Motion執行動作
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNTAxMDAxNTMsLTkwMTI4MDgyNywxOT
c2OTMxOTI4LC0yMDMzNzQ3NzQ3LC0xOTgxNDk4OTk1XX0=
-->