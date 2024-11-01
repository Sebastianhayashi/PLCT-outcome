# 10 月产出

## 日志轮转测试代码

- 仓库：https://github.com/Sebastianhayashi/log_rotation
- issue1:https://github.com/Sebastianhayashi/log_rotation/issues/1
- issue2:https://github.com/Sebastianhayashi/log_rotation/issues/2

仓库结构：

```
yuiyuuhayashi@MacBook-Air log_rotation % tree
.
├── Archive
│   └── folder_move.sh -> 文件嵌套脚本
├── CMakeLists.txt
├── README.md
├── ROS log report.md -> 调研报告
├── config
│   └── spdlog_config.yaml 
├── launch
│   └── log_test_node_launch.py
├── package.xml
├── src
│   └── log_test_node.cpp
└── start.sh -> 测试脚本

5 directories, 9 files
```
## eigen

- 仓库：https://github.com/Sebastianhayashi/eigen
- issue1：https://github.com/Sebastianhayashi/eigen/issues/1
- eigen 库测试结果：https://github.com/Sebastianhayashi/eigen.git

> eigen 库测试耗时两个工作日。

仓库结构：

```
yuiyuuhayashi@MacBook-Air eigen % tree
.
├── README.md
├── compilation test
│   ├── README.md
│   ├── test-1
│   │   ├── README.md
│   │   └── vector_test.s
│   ├── test-2
│   │   ├── README.md
│   │   └── vector_test.s
│   └── test-3
│       ├── README.md
│       └── vector_test.s
└── test_result
    ├── test-10.29-11:06
    │   ├── README.md
    │   └── eigen.log
    ├── test-10.29-16:40
    │   └── README.md
    └── test-10.30-11.1
        ├── CTestCostData.txt
        └── LastTest.log

9 directories, 13 files
```

## Cartographer 基本调研

- 仓库：https://github.com/Sebastianhayashi/Cartographer

仓库结构：

```
yuiyuuhayashi@MacBook-Air Cartographer % tree
.
├── README.md
└── 调研报告.md

1 directory, 2 files
```

## gazebo

仓库如下：

- https://github.com/Sebastianhayashi/ign-cmake0
- https://github.com/Sebastianhayashi/ign-cmake2
- https://github.com/Sebastianhayashi/ign-math6
- https://github.com/Sebastianhayashi/Freeimage -> 根据 24.03 进行优化
- https://github.com/Sebastianhayashi/ign-common3
- https://github.com/Sebastianhayashi/Ignition-msgs5
- https://github.com/Sebastianhayashi/ign-transport8
- https://github.com/Sebastianhayashi/ign-fuel-tools4
- https://github.com/Sebastianhayashi/qwt
- https://github.com/Sebastianhayashi/ogre
- https://github.com/Sebastianhayashi/sdf9

> 产出编译脚本/对其版本/协助韩老师