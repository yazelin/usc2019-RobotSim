# 課程設計
## 目的
> - 畢業 > 就業 > 創業
> - 取得就業即戰力

## 方法
> - 以實際專案進行的順序擬定大綱。
> - 並依大綱依序學習必要技能。

1. 前期規劃 (略)
  - 了解現況
  - 如何以自動化替代人力
  - 初步構想
2. 初步模擬 (一、二)
  - 流程
  - 空間配置(干涉)
3. 實機測試 (三、四)
  - 硬體安裝、微調
  - 軟體測試、重構
4. 建置完整系統 (五、六)
  - 周邊設備整合
  - 整合測試
  - 驗收
 
## 步驟
### 一、RobotSim基礎(3/13) [教學頁面](./1RobotSimBasic.html)
1. 課程大綱
2. 手臂基本介紹
3. RobotSim環境及基本操作
  - 下載-安裝-試用 [參考影片](https://www.youtube.com/watch?v=xv4v_fOwAC0&index=20&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo)
  - 教點-程式-模擬 [參考影片](https://www.youtube.com/watch?v=4Gk7K88B10c&index=21&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo)
  - 設定Tool-更新點位-模擬動作 [參考影片](https://www.youtube.com/watch?v=NLA6A_qWDgs&index=22&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo)
  - 設定Base-設定手臂-匯出程式 [參考影片](https://www.youtube.com/watch?v=izkk5MW-FeY&index=23&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo)
4. RobotSim基礎程式
  - 變數
  - 設定
  - 動作
  - 流程控制

### 二、RobotSim專案制作(3/27) [教學頁面](./2RobotSimProject.html)
1. RobotSim完整專案
  - RobotSim程式設計擴充 C# [參考](https://yazelin.github.io/cnu2018-RobotSim/)
  - 自訂函式/修改功能
2. RobotSim匯出 並匯入WorkVisual專案

### 三、手臂操作訓練及KRL程式語言(4/10) [教學頁面](./3KukaRobotLanguage.html)
1. 手臂安全及基本操作 [參考文件](http://www.wtech.com.tw/public/download/manual/kuka/krc4/KUKA%20KSS%208.3%20for%20End%20User.pdf)
2. WorkVisual KRL 程式語言 [參考文件](http://www.wtech.com.tw/public/download/manual/kuka/krc4/KUKA%20KRL-Syntax%208.x.pdf)
  - 變數
  - 常用函式
  - 動作指令
  - 流程控制

### 四、WtFramework 開發框架(4/24) [教學頁面](./4WtFramework.html)
1. WtFramework開發框架介紹 [參考文件](https://docs.google.com/document/d/1Szhp_FcrscaeyZ9ZzW3MuSqA4tz6_ZzheJut4y5GJkQ/edit?usp=sharing)
  - Core
  - Action
2. 安裝
3. 網路通訊 EKI 
  - Server
4. 練習

### 五、自動化專案實作 一(5/08) [教學頁面](./5Project1.html)
1. WtFramework 自動化專案 實作
  - PC端 為主控端 C#
  - Robot端 為被控設備 KRL
  - UI素材 [下載](./src/AssetsPack.unitypackage)

### 六、自動化專案實作 二(5/22) [教學頁面](./6Project2.html)
1. WtFramework 自動化專案 實作
  - PC端 為主控端 C#
  - Robot端 為被控設備 KRL

## 環境需求
- Unity 2017 (3D環境) 
- RobotSim (模擬手臂)
- Visual Studio (C# 編輯器)
- KUKA KR3 (機器手臂)
- WorkVisual (KRL 編輯器)

## 學習成果
- 自動化系統專案開發流程
- Unity、VisualStudio、VisualWork 軟體操作
- C#、KRL 程式語言撰寫
- 操作KUKA機器手臂

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQzNTYxMTMyNSwtOTc0NzI0NDc3LDEzMz
c0MDE0NDcsLTE5NDc3NzU2OSwtNDQxMzIzOTIwLDE2NjEwOTIy
NzIsLTIwMDMzOTI0MDgsLTE5MjkzMzU5OTYsLTcyNTQwNTY5OS
w2NDg3NzAwNywtMTExMTcyODgyNSwyMDQzMDg2MTg2LDE0ODQw
NzQ4NzksLTk0NDc0MzY4MSw1Mzg2ODQyNTIsMTU5ODU4NDk4Ni
wxMjMwNjk1NTUxLDM2MDY2ODQwMCwxMTkwNTQ3NCwtMTc3MzY4
MDMxXX0=
-->