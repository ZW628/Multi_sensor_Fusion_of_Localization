# Multi_sensor_Fusion_of_Localization
深蓝学院_多传感器融合定位_课程学习记录

# 课程内容：
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/%E8%AF%BE%E7%A8%8B%E5%86%85%E5%AE%B9.jpg)

# 前端里程计方案：
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/%E5%89%8D%E7%AB%AF%E9%87%8C%E7%A8%8B%E8%AE%A1%E6%96%B9%E6%A1%88.png)

## 里程计工程框架实现：
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/%E9%87%8C%E7%A8%8B%E8%AE%A1%E5%B7%A5%E7%A8%8B%E6%A1%86%E6%9E%B6%E5%AE%9E%E7%8E%B0.png)


# 项目实现：

# 实验过程记录：

## 前端里程计之初试：
建立工作空间sl04_ws；

roslaunch lidar_localization front_end.launch

rosbag play kitti_2011_10_03_drive_0027_synced.bag -r 0.3

因为地图都在内存中，所以运行会很卡，播放速度可调慢些；

运行完显示全局点云地图：

![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/4.1.jpg)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/4.2.png)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/4.3.png)

## 前端里程计之代码优化：
上一节里，关键帧点云和全局地图都是放在内存里

本节改进：每产生一个关键帧就把它存放在硬盘里，然后把点云释放掉，全局地图默认不生成，必须主动发送指令才会生成，生成之后会把地图保存成pcd文件，并在rviz上显示。

地图展示：
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/5_1.png)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/5_2.png)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/5_3.png)

从上面这张图可见：地图有重影（激光雷达运动畸变导致）、里程计有累计误差（需消除）

![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/5_4.png)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/5_5.png)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/5_6.png)

## 闭环修正：
通过消除运动畸变、累计误差，后端优化和闭环修正后的地图，改善了不少

地图展示：
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/11.1.PNG)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/11.2.PNG)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/11.3.PNG)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/11.4.PNG)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/11.5.PNG)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/11.6.PNG)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/11.7.png)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/11.8.png)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/11.9.png)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/11.10.png)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/11.11.png)

明显可见，重影消失了

## 基于地图的定位：
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/14_1.PNG)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/14_2.PNG)
![image](https://github.com/ZW628/Multi_sensor_Fusion_of_Localization/blob/main/14_3.gif)

