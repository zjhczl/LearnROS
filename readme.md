# ROS
## 安装ros
在 Ubuntu 20.04 (Focal Fossa) ARM64 架构上安装 ROS 1（Robot Operating System）通常涉及以下步骤。以安装 ROS Noetic（适用于 Ubuntu 20.04 的版本）为例，请按照以下步骤操作：

1. **配置您的 Ubuntu 软件仓库**  
   确保您的 Debian 软件包索引是最新的，并且仓库允许 "restricted"、"universe" 和 "multiverse"。

2. **设置 ROS 源**  
   首先，您需要添加 ROS 的源：

   ```sh
   sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
   ```

3. **添加密钥**  
   然后，您需要添加 ROS 的密钥：

   ```sh
   sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
   ```

   如果您遇到问题，也可以尝试使用 `curl`：

   ```sh
   curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
   ```

4. **安装**  
   更新您的软件包索引，然后安装 ROS。您可以选择安装完整版、桌面版或基础版。完整版包含了 ROS、rqt、机器人模型、仿真、导航等：

   ```sh
   sudo apt update
   sudo apt install ros-noetic-desktop-full
   ```

   如果您只需要基础功能，可以安装 `ros-noetic-ros-base`。

5. **初始化 rosdep**  
   在使用 ROS 之前，您需要初始化 `rosdep`。`rosdep` 可以方便地安装系统依赖项，以及编译和运行一些核心组件时所需的东西：

   ```sh
   sudo apt install python3-rosdep
   sudo rosdep init
   rosdep update
   ```

6. **环境设置**  
   您需要将 ROS 环境变量添加到您的 shell 会话。这样做的最简单方法是将以下行添加到您的 `.bashrc`：

   ```sh
   echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
   source ~/.bashrc
   ```

   如果您使用的是 zsh 或其他 shell，请将上述命令中的 `.bashrc` 替换为相应的配置文件。

7. **安装 rosinstall**  
   `rosinstall` 是在 ROS 工作空间中使用的常用命令行工具：

   ```sh
   sudo apt install python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
   ```

完成以上步骤后，ROS Noetic 应该已经安装在您的 Ubuntu 20.04 ARM64 系统上了。您可以通过运行一些基本的 ROS 命令来测试安装，例如 `rosversion -d` 来检查当前安装的 ROS 版本。
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
