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
  
  ```
IP 127.0.0.1 
Port 54600
前 <Data><Direction>1</Direction></Data>
後 <Data><Direction>2</Direction></Data>
左 <Data><Direction>3</Direction></Data>
右 <Data><Direction>4</Direction></Data>
夾 <Data><Direction>5</Direction></Data>
  ```
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTY5NTg0OTg0LDQ0NDI1MDM5LDE3Mzc5ND
YxNTksMTQ0MzQ4MTc0NSw3Mjk1MDY3NjEsMTQyNjk0NDk1MSwt
MTgzMDExNDc2NSwxNzYyMDQ3MzQwLC0zNDIyNDI3NTMsMTE3NT
EyNzg1NF19
-->