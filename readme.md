# ROS

## 基本命令
### roscore
启动ros master
### rosrun
启动节点

```
rosrun 功能包 节点
rosrun turtlesim turtlesim_node 
```

### rqt_graph
了解系统全貌

### rosnode
显示系统节点

### rostopic

发布一次数据
```
rostopic pub /turtle1/cmd_vel geometry_msgs/Twist "linear:
  x: 1.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 0.0" 
```
循环发送数据(以10赫兹的频率发送topic)
```
rostopic pub -r 10 /turtle1/cmd_vel geometry_msgs/Twist "linear:
  x: 1.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 1.0" 
```

### rosmsg
消息相关
```
rosmsg show turtlesim/Pose 
float32 x
float32 y
float32 theta
float32 linear_velocity
float32 angular_velocity

```

### rosservice
```
rosservice list 
/clear
/kill
/reset
/rosout/get_loggers
/rosout/set_logger_level
/spawn
/teleop_turtle/get_loggers
/teleop_turtle/set_logger_level
/turtle1/set_pen
/turtle1/teleport_absolute
/turtle1/teleport_relative
/turtlesim/get_loggers
/turtlesim/set_logger_level
```
调用服务

```
rosservice call /spawn "x: 0.0
y: 0.0
theta: 0.0
name: 'zj'" 

```
### rosbag

录制数据
```
rosbag record -a -O zj_record

```
-a是录制所有数据
-O是指定录制包的名称

使用包
```
rosbag play zj_record.bag 

```
## 基本流程


-工作空间
--src
--build
--devel
--install

### 创建工作空间
```
mkdir -p ~/ros_ws/src
cd ~/ros_ws/src
catkin_init_workspace 

```
### 编译空间
```
cd ~/ros_ws
catkin_make
```
```
catkin_make install
```
这个命令会产生install文件夹

### 设置环境变量
```
source devel/setuo.bash
```
### 检查环境变量
```
echo $ROS_PACKAGE_PATH
```
### 创建功能包
catkin_create_pkg <pkg_name> <dep1> <dep2>
```
cd ~/ros_ws/src
catkin_create_pkg test_pkg std_msgs rospy roscpp
```
### 编译功能包
```
cd ~/ros_ws
catkin_make
source ~/ros_ws/devel/setup.bash
```