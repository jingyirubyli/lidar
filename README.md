# Livox LiDAR 学习笔记

Q: 不使用Livox hub可以实现多台雷达数据同步采集吗(多台雷达至一台电脑)

官方用户手册有写出多台雷达数据采集的方法，但里面明确写出需要用到Livox hub硬件。https://www.livoxtech.com/3296f540ecf5458a8829e01cf429798e/downloads/20190218/Livox%20Hub%20Quick%20Start%20Guide_v1.0_20190218.pdf
如果手边没有Livox hub设备，通过其他的硬件比如交换机或路由器之类的，能实现多台雷达数据传输到一台电脑的目的吗？如果可以，是用Livox-SDK接收数据还是怎么操作呢？
还是说Livox的设备只能通过Livox hub硬件才能实现多台雷达数据的同时采集？

A: 不需要适用Livox Hub(当前已停产) 也可以将多台雷达的数据传输到同一个电脑中，只需要将雷达设置在同一个网段下，并和电脑同时连接到一个交换机或者路由器上即可。多雷达数据采集可通过ros driver实现，启动livox lidar launch文件，默认配置可连接网段内全部雷达，如果只需要连接其中一两个，具体参考ros驱动的config配置。

时间同步: https://livox-wiki-cn.readthedocs.io/zh-cn/latest/tutorials/other_product/timestamp_sychronization.html

Q: 如果电脑中有两个进程需要访问两台不同的激光雷达，调用这个Livox-SDK会出现端口占用的情况这个怎么解决

未解决

Q: 在使用两台雷达时，roslaunch livox_ros_driver livox_lidar_rviz.launch, 在rviz中看到来自两个雷达的点云交替的闪，不能一帧点云包含两个雷达的数据，
请问如何拼接俩台或多台设备的数据？

A: 多台雷达需时间同步才可以同步显示.参考上面链接.

如果需要使用两个mid-360,运行一个节点输出两个雷达的点云数据: 更改config文件夹下MID360_config.json文件，在lidar_configs选项中添加两个雷达的ip即可

多雷达数据采集: https://livox-wiki-cn.readthedocs.io/zh-cn/latest/tutorials/other_product/multiple_lidars_capture.html

参考: https://blog.csdn.net/qq_33912182/article/details/140353115

注:多激光雷达外参自动标定算法开源(官方) https://www.livoxtech.com/cn/showcase/8
另一个作者:https://github.com/GDUT-Kyle/MULTI_LIDARs_CALIBRATE

Q: 两个mid360雷达在同一网络下，不同主机，不能同时运行ros driver程序,主机1启动driver程序后，主机2在启动程序时，会造成主机1程序死掉。雷达ip分别为：192.168.1.124和192.168.1.143主机ip分别为：192.168.1.191和192.168.1.192

https://github.com/Livox-SDK/livox_ros_driver2/issues/140

https://github.com/Livox-SDK/livox_ros_driver2/issues/102

Q: 使livox雷达与Ubuntu18.04电脑进行无线通信

https://blog.csdn.net/m0_61281991/article/details/124439612
