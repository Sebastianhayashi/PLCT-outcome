# 会议

## Cartographer

> 进度：调研完成，解决环境相关问题

目前调研到将 ros1 上的 bag 转成 ros2 的格式，使用 `rosbags-convert` 指令实现，但是发现转完格式的 bag 无法运行。

还有很多的问题需要解决，如：

```
(rosbags) debian@revyos-lpi4a:~$ ros2 bag info TB3_WAFFLE_SLAM_converted.bag
[ERROR] [1732526757.678742652] [rosbag2_storage]: No storage id specified, and no plugin found that could open URI
No plugin detected that could open file TB3_WAFFLE_SLAM_converted.bag
(rosbags) debian@revyos-lpi4a:~$ ros2 bag play TB3_WAFFLE_SLAM_converted.bag
[ERROR] [1732526779.226591610] [rosbag2_storage]: No storage id specified, and no plugin found that could open URI
No storage could be initialized from the inputs.
```

这是由于在 revyos 上的 ros2 环境配置问题，下一步将这些基本的问题解决，然后在 lpi4a 上基于 revyos 测试 cartographer

### 问题

- 确定架构以及系统
  - 没有确定的话就是 lpi4a + revyos
- 确定 ROS2 版本
- 建模程度

## 论文分享

> 进度：阅读了论文一半

主要讲的是如何赋予视觉运动机器人在多样化的开放世界场景中操作的泛化能力，主要是围绕 Maniwhere 通用框架，专为视觉强化学习设计，主要是为了解决视觉机器人在实际任务环境中会遇到的多重视觉干扰。

## 工具集调研

任务关闭，任务结束。

## Jazzy 任务

还没有开始

