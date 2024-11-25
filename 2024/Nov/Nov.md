# 产出清单

## 日志说明会议

仓库：https://github.com/Sebastianhayashi/log_rotation


```
➜  log_rotation git:(main) tree
.
├── 11.16 meeting.md
├── Archive
│   ├── CMakeLists.txt
│   ├── ROS log report.md
│   ├── config
│   │   ├── log_config.yaml
│   │   └── spdlog_config.yaml
│   ├── folder_move.sh
│   ├── include
│   │   └── ros2_log_rotation
│   │       ├── compression_util.hpp
│   │       ├── config.hpp
│   │       └── logger_manager.hpp
│   ├── launch
│   │   └── log_test_node_launch.py
│   ├── package.xml
│   ├── scripts
│   │   └── log_rotation_gui.py
│   ├── spdtest
│   │   └── spdtest.cpp
│   ├── src
│   │   ├── Archive
│   │   │   ├── log_rotation.cpp
│   │   │   └── log_test_node.cpp
│   │   ├── compression_util.cpp
│   │   ├── compression_util.hpp
│   │   ├── config.cpp
│   │   ├── logger_manager.cpp
│   │   ├── logger_manager.hpp
│   │   └── main.cpp
│   ├── start.sh
│   ├── test.sh
│   └── tests
│       ├── CMakeLists.txt
│       ├── test_compression.cpp
│       └── test_logger.cpp
├── README.md
└── img
    └── ros2_logging_architecture.png

12 directories, 28 files
```

> 产出说明：增加部分日志系统测试文件，以及增加会议内容。

## 工具集调研

仓库：https://github.com/Sebastianhayashi/RV-Tools.git

```
➜  ~ tree RV-Tools
RV-Tools
├── README.md
├── RISmartPorting.md
├── RISmartPorting_test.md
├── img
│   ├── 1.png
│   └── 2.png
├── riscv-tests.md
└── test_log
    └── oe.log

3 directories, 7 files
```