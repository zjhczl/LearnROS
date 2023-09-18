# 矿卡测试

北云ip:192.168.2.151
## 准备
1.连接网线和typec线，检查网络
2.切换路径到chasiss_ws
```
./can_driver.sh #建立can通讯
```
```
candump #打印can线数据
```
3.
```
roslaunch bynav_ros_driver connect_net.launch #接入差分

```
4.
```
rostopic echo /bynav/inspva #打印inspva
```

5.
```
rostopic echo /bynav/gpgga #打印gpgga
```

## 录制路线

1.把车开到起点，等待5s以上
2.录制数据包
```
rosbag record -a
```
3.把包改名为record_ros_data.bag移动到chasiss_ws/src/startingup_ros/data/bag

4.修改矿卡档位
修改chasiss_ws/src/startingup_ros/data/param/vehicle_info.yaml

4.初始化起点
```
roslaunch startingup_ros autudriver_gps_init_pose.launch #
```

5.生成轨迹
```
roslaunch startingup_ros autudriver_make_lane.launch 
```

## 运行路线
1.仿真显示轨迹
```
roslaunch startingup_ros autudriver_dispaly_lane.launch
```
2.实际运行轨迹
```
roslaunch startingup_ros autudriver_tracking_navi.launch
```
3.运行底盘
```
roslaunch chasiss_drievr chasiss_driver.launch
```


## 生成反向轨迹包

```
roslaunch btreverse_record_bag reverse_record_bag.launch
```

## 引导停车装载点设置
```
rostopic pub /load_unload_goal_point
```
