## Basic operation

## Industrial Robot Introduction

### 6-axis Robots
![Image](../img/RobotSystem.jpg)

### Axis
- A1~A6 

![Image](../img/RobotAxis.jpg)

### Space
- Base Space

![Image](../img/RobotCoordinateSystem.jpg)

- Tool Space

![Image](../img/Tool.jpg) 

### The basic concepts of robotics lon-line earning 
- Embeded RobotSim simulation on WebPlaer
-   [RobotSim WebPlayer](http://www.wtech.com.tw/robotsim/demo)
- The basic concepts of robotics includes
	- Coordinate systems
		- WORLD
		- BASE
		- TOOL    
	- Jogging Mode
		- Cartesian jogging with XYZ ABC according to the selected coordinate system
		- Axis-specific jogging
	- Motion type
		- PTP
		- LIN
		- CIRC
	- Axis Range Limitation
		- A1~A6
	- Teaching and Programing
		- Teach several points to create a robot motion path
		- Program robot running on the path repeatly by Loop function

## Basic operation 

### Download, installation and testing 
<iframe width="560" height="315" src="https://www.youtube.com/embed/xv4v_fOwAC0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- Download link [link](http://www.wtech.com.tw/downloadrobotsim)
- Reference media [link](https://www.youtube.com/watch?v=xv4v_fOwAC0&index=20&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

### Teaching, programing and simulation
<iframe width="560" height="315" src="https://www.youtube.com/embed/4Gk7K88B10c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- Reference media [Link](https://www.youtube.com/watch?v=4Gk7K88B10c&index=21&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

### Adding a tool
<iframe width="560" height="315" src="https://www.youtube.com/embed/NLA6A_qWDgs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- Reference media [Link](https://www.youtube.com/watch?v=NLA6A_qWDgs&index=22&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

### Select tool, base, robot and program
<iframe width="560" height="315" src="https://www.youtube.com/embed/izkk5MW-FeY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- Reference media [Link](https://www.youtube.com/watch?v=izkk5MW-FeY&index=23&list=PLYLTPJkULAAZZuNW2s2tX-KWQOus7sAAo).

## RobotSim Programming
-  Value
  - Bool、Int、Float、String
  - Set、Add、Sub、Mut、Div

![Image](../img/Value.png) 
-  Motion
  - Base、Tool、Speed
  - PTP 、LIN、CIRC

![Image](../img/Motion.png) 
-  Flow
  - Loop、For-Loop、Wait Time
  - If-Else、While、Switch-Case

![Image](../img/Flow.png)

## Excises
- import RobotSim [download page](http://www.wtech.com.tw/robotsim)
- start Robot window、Program window、Controller window
- Add a empty space scene

![Image](../img/EmptyRobotSimScene.png)
- Select a Robot

![Image](../img/AddRobot.png)
- Select a  Program

![Image](../img/AddProgram.png)
- Select Controller

![Image](../img/AddController.png)
- Link Robot、Controller、Program

![Image](../img/LinkProgramRobot.png)
- Set up main camera

![Image](../img/MainCamera.png)
- Add point #1 and point #2.

![Image](../img/AddPoint.png)
- Add motion type: PTP、LIN

![Image](../img/AddPTP.png)
![Image](../img/AddP1.png)
- Set up parameters、using FOR-LOOP for flow control

![Image](../img/AddINTI.png)
![Image](../img/AddFORLOOP.png)
- Set up  SPEED、add WAIT SEC 

![Image](../img/AddSPEED.png)
![Image](../img/AddWAITSEC.png)

## Outputs
![Image](../img/Week1Program.png)
![Image](../img/Week1DEMO.gif)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgzMTI3ODYyNiwxMTkxODY2MjY4LDExOT
E4NjYyNjgsMTE5MTg2NjI2OCwxMTkxODY2MjY4LDExOTE4NjYy
NjgsLTE3NTk3Mjc4NjEsMTYyNzk0NTIwOCwtNTQ2NjI4MzMsMT
I3MTM5MzA3MSwtMTIxNjI5MDAzNCwtMTk3NzQxMzgyNiwzMTY2
NzY2NzcsOTY2MzE1NzQ5LDE2MjY5OTQwNTYsMTAwMTg4NjM0Ny
wzNjc4MDU1ODgsLTU0NzU2NjM0NCw1MDc2NzYwMDksLTExMzI3
MTA5Nl19
-->