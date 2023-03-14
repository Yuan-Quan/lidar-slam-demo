# 激光SLAM理论与实践

实验1: 激光SLAM建图

## 工作空间的准备

进入工作空间

```sh
cd source/repos/lidar-slam-demo
```

编译工作空间

```sh
catkin_make
```

## 启动仿真环境

在进入工作空间后, 

```sh
roslaunch ucar_bringup start_simulation.launch
```

将会启动仿真环境  
  
此时仿真会提供雷达点云数据

新开一个终端, 进入工作空间, 运行

```sh
rostopic echo /scan
```

也会提供里程计

```sh
rostopic echo /odom
```

也会接收速度指令

```sh
roslaunch teleop_twist_joy teleop.launch
```

## 运行建图算法

### Gmapping

新开一个终端, 进入工作空间, 运行:

```sh
roslaunch ucar_navigation gmapping.launch
```

通过遥控器控制小车, 完成建图

保存地图:  
新开一个终端, 进入工作空间,  
进入到想保存地图文件的地方, 运行:

```sh
rosrun map_server map_saver
```

### Cartographer

关闭全部节点之后, 重新启动仿真环境

新开一个终端, 进入工作空间, 运行:

```sh
roslaunch ucar_navigation cartographer_mapping.launch
```

通过遥控器控制小车, 完成建图

保存地图:  
新开一个终端, 进入工作空间,  
进入到想保存地图文件的地方, 运行:

```sh
rosservice call /finish_trajectory 0
rosrun map_server map_saver
```
