# xunjicar-code
A413循迹小车考核代码

循迹小车考核项目
=

目录
--
1.考核题目解析
2.硬件设计
3.软件设计

##考核题目解析：
--
1.要求：制作一个蓝牙循迹小车，在蓝牙指令控制下在图中到达目标要求点位，并返回出发点代表任务完成。
2.硬件设计要求：要求各个模块均在嘉立创EDA上打板制作，主控模块及蓝牙模块除外；小车尺寸在25cm*25cm之内
3.软件设计要求：针对任务一，在发出指令后小车按要求到达指定点位后，停留2S之后返回，证明一次任务完成，重复三次证明任务一成功

##硬件设计：
--
模块主控选择：乐鑫科技的ESP32
电机驱动模块选择：两个tb6612，控制四轮形成四驱小车
循迹模块选择：按照TCRT5000形式制作，并外加补光灯，保证循迹效果
电源模块：外部供电选择12V移动电源，选择MP2315DC-DC开关电源，降压电路实现12V-5V降压，5V电压为单片机及TB6612启动供电；12V为tb6612的输入电压；5V--3V3选择LM1117LDO线性稳压芯片，为蜂鸣器，OLED屏幕外设供电
外部配件：
使用麦克纳姆轮便于实现小车平移；整体结构使用塔式小车
循迹位置放置：小车结构为正方形底座，四个循迹在前后左右四个方向

##软件设计：
--
整体思路：利用麦轮平移功能，在X方向上前行，左侧循迹进行计数功能，到达X坐标后停止进入中断，利用麦克纳姆轮进行向左平移，启用后侧循迹，进行计数，到达指定y坐标后停止。
向右平移，利用前后循迹卡位置，当返回值为0时，开始向后平移，当左侧循迹返回值为0时，停车，实现任务一。
