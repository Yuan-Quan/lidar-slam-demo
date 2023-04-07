#  实验2 - 2D激光雷达运动畸变补偿

## 操作步骤

1. 新建工作空间

```sh
mkdir -p lidar-undistortion-demo/src

```

2. 下载激光雷达与imu的驱动


```sh
cd lidar-undistortion-demo/src

git clone https://github.com/YDLIDAR/ydlidar_ros_driver.git

git clone https://github.com/SHUNLU-1/fdilink_ahrs.git
```

3. 编译并测试IMU与雷达

构建工作空间

```sh
cd ..
catkin_make
```

修改IMU与激光雷达的launch文件中， port参数为相应的串口名称

```text
<param name="port"  value="/dev/ttyACM0"/>

...

<param name="port"         type="string" value="/dev/ttyUSB0"/> 
```

启动并测试IMU与激光雷达

```sh
roslaunch ydlidar X3.launch
roslaunch fdilink_ahrs ahrs_data.launch

rostopic echo scan
rostopic echo imu
```

4. 畸变去除

拉取畸变消除节点的源代码

```sh
git clone https://github.com/Deego-Robotics/2d_lidar_undistortion.git
```

重命名话题

设置激光雷达节点发布话题名称为scan_raw

```xml
<remap from="scan" to="scan_raw" />
```

设置畸变去除节点接受话题scan_raw

```xml
<param name="lidar_topic" value="/scan_raw"/>
```

修改雷达的launch文件使其启动imu与畸变补偿节点

构建工作空间， 启动节点

```sh
catkin_make
roslaunch ydlidar X3.launch
```

即可在rviz中看到, 经过畸变补偿之后的点云
