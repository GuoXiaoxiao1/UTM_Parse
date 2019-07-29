# UTM_Parse


# README

## 引言

本实验为经纬度UTM投影实验，重点是要掌握UTM投影方法。实验中，首先要对导航串口数据进行解析，得到车辆实时的经纬度数据，然后采用UTM投影方法将大地经纬度坐标转换为UTM平面坐标，为后续差分导航路径规划模块做准备。本实验包含2个ROS包和1个.py文件：xfgps_parse、xfutm_parse和main.py。其中，xfgps_parse的ROS包为差分导航驱动模块，负责读取导航串口数据并解析，将解析后的实时经纬度、高度、航向角、RTK状态、车速等信息发送给xfutm_parse节点。xfutm_parse的ROS包为UTM投影模块，负责将接收到的车辆实时经纬度信息转换为UTM平面坐标，并发送给UI界面显示。main.py为UI控制界面，负责转换前后大地经纬度坐标值、UTM平面坐标值、航向角、RTK状态、车速、搜星数等信息的显示，同时可将转换前后两种坐标值的位置信息存储为相应的地图文件。各ROS包之间的消息通信如下图所示：

![node](https://raw.githubusercontent.com/GuoXiaoxiao1/UTM_Parse/master/UTM/Node.png)

## 依赖

- ros kinect(Ubuntu 16.04)
- pyqt5

## 编译

```
% cd UTM_Projection/src
% sudo chmod -R 777 *
% cd ..
% catkin_make
    
```

## 运行

本实验有两种运行方式，既可在线运行，也可离线运行。在线运行是指直接从导航设备的串口读取数据并解析，因此需要运行导航驱动xfgps_parse的ROS包，利用其来提供解析后的车辆实时经纬度、航向角、RTK状态、车速等信息；离线运行是指在有采集好的解析后导航数据的前提下，可通过播放bag包的形式来提供实时的经纬度信息。

1.在线运行：

```
% cd UTM_Projection
% source devel/setup.bash
% roslaunch xfutm_parse utm_parse_online.launch

```

2.离线运行：

```
% cd UTM_Projection
% source devel/setup.bash
% roslaunch xfutm_parse utm_parse_offline.launch

```

- 在UI界面中，点击“Start”按钮,开始进行经纬度坐标与UTM平面坐标的转换，并分别显示转换前后的坐标值和其他重要的导航参数。
- 点击“Save”按钮可分别对转换前后两种坐标值的位置数据进行保存。地图文件的存储路径默认为.py文件所在目录的map文件夹下。
- 经纬度地图的存储文件默认为UTM_LonLat.txt文件，转换后的UTM平面坐标的地图文件默认为UTM_XY.txt文件。因此在需要多次操作保存地图文件时，应先删除上次保存的地图，否则新保存的地图点会以追加的方式补充在原地图文件中。
- 更多UI界面操作信息与显示信息可参考本实验的实验指导书中示例软件展示部分。

##示例demo

![demo](https://raw.githubusercontent.com/GuoXiaoxiao1/UTM_Parse/master/UTM/UI.png) 

##联系我们

如果您有相关实验课件的其他需要，或向我们反馈一些本实验存在的bug,或想向我们提供一些特殊场景的实验数据，请联系我们：

```
Email: lemonxiaoxiao9@163.com

```

注：反馈数据的格式应为rosbag包
