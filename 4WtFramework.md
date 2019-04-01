## 四、WtFramework 開發框架
1. WtFramework開發框架介紹
  - [架構圖](./src/Wt專案架構圖.pdf)
  - [流程圖](./src/WtFrameworkFlowCharts.pdf)
  - Core
  - Action
2. 安裝
  - 於 WorkVisual 內點選 File/Cataloghandling...
  - 於 Catalogs 視窗點選 KRL Templates 後按 > 按鈕 加入功能
  - ![Image](./img/AddKRLTemplates.png)
  - 將 WtFramework.zip 解壓縮後將 KUKA Templates資料夾 覆蓋 C:\Users\User\Documents\KUKA Templates 資料夾
3. 網路通訊
  - EKI [參考文件](http://www.wtech.com.tw/public/download/manual/kuka/krc4/KST-Ethernet-KRL-21-En.pdf)
  - Server
4. 練習
5. 夾娃娃機PC端操作介面
  - PC端手臂模擬程式
 <iframe width="560" height="315" src="https://www.youtube.com/embed/W62LbDkruTw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
 
  模擬程式下載: [https://github.com/yazelin/usc2019-RobotSim/raw/master/src/Play.zip](https://github.com/yazelin/usc2019-RobotSim/raw/master/src/Play.zip)  
解壓縮後執行 USC2019RobotSim.exe
  ```
IP 127.0.0.1 
Port 54600
前 <Data><Direction>1</Direction></Data>
後 <Data><Direction>2</Direction></Data>
左 <Data><Direction>3</Direction></Data>
右 <Data><Direction>4</Direction></Data>
夾 <Data><Direction>5</Direction></Data>
  ```
  - 操作介面範例
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NDI3MDkzNTksNDQ0MjUwMzksMTczNz
k0NjE1OSwxNDQzNDgxNzQ1LDcyOTUwNjc2MSwxNDI2OTQ0OTUx
LC0xODMwMTE0NzY1LDE3NjIwNDczNDAsLTM0MjI0Mjc1MywxMT
c1MTI3ODU0XX0=
-->