# 十二月产出

## 主要任务

- Jazzy 软件包构建及其衍生工具开发和测试
- rc_dynamics_api 构建报错分析

## Jazzy 移植

### 软件包构建产出

- 成功安装的包总数：263
- 成功构建数量：344

- [repo](https://eulermaker.compass-ci.openeuler.openatom.cn/api/ems1/repositories/jazzy_ament_package/openEuler%3A24.03-LTS/x86_64/)
- [构建页面](https://eulermaker.compass-ci.openeuler.openatom.cn/project/overview?osProject=jazzy_ament_package)
- [软件包支持详细表格](https://github.com/Sebastianhayashi/openEuler-Jazzy-Porting)

### 产出报告

```
➜  openEuler-Jazzy-Porting git:(main) tree
.
├── Bloom-Reports
│   ├── Bloom_tool_research.md
│   ├── Porting_rosdep.md
│   ├── img
│   │   ├── 1.png
│   │   ├── 2.png
│   │   ├── 3.png
│   │   ├── 4.png
│   │   ├── 5.png
│   │   ├── 6.png
│   │   ├── 7.png
│   │   └── 8.png
│   ├── porting_bloom_on_openEuler_detectable.md
│   └── rosdep-oe_report.md
├── Jazzy-porting-reports
│   ├── Complie_LTTng-Tools_Report.md
│   └── Jazzy-porting-reports.md
├── README.md
└── Scripts
    ├── Gitee
    │   ├── make_gitee_repos_public.py
    │   └── upload_to_gitee.py
    └── openEuler
        ├── batch_process_packages.sh
        ├── fetch_ros_packages.py
        └── process_ros_packages.sh

7 directories, 20 files
```

### 本月更新

报告：

- Complie_LTTng-Tools_Report.md -> LTTng-Tools 工具缺失报告
- Jazzy-porting-reports.md -> rot 工具基本介绍报告


脚本：
- make_gitee_repos_public.py
- upload_to_gitee.py
- batch_process_packages.sh
- fetch_ros_packages.py
- process_ros_packages.sh

## rot 工具

```
➜  ros_openeuler_tool git:(main) tree
.
├── README.md
├── requirements.txt
├── ros_openeuler_tool
│   ├── __init__.py
│   ├── analyze_dependencies.py
│   ├── batch_process.py
│   ├── cli.py
│   ├── clone_repos.py
│   ├── extract_unresolved_dependencies.py
│   ├── list_missing.py
│   ├── make_public.py
│   ├── map_yum_rosdep.py
│   ├── process_packages.py
│   ├── requirements.txt
│   ├── ros_openeuler_tool
│   │   └── extract_unresolved_dependencies.py
│   ├── ros_openeuler_tool.egg-info
│   │   ├── PKG-INFO
│   │   ├── SOURCES.txt
│   │   ├── dependency_links.txt
│   │   ├── entry_points.txt
│   │   ├── requires.txt
│   │   └── top_level.txt
│   ├── setup.py
│   ├── sync_gitee.py
│   └── update_yum_mapping.py
├── ros_openeuler_tool.egg-info
│   ├── PKG-INFO
│   ├── SOURCES.txt
│   ├── dependency_links.txt
│   ├── entry_points.txt
│   ├── requires.txt
│   └── top_level.txt
├── setup.py
└── update_rosdep_yaml.py

5 directories, 31 files
```

### 产出说明

支持以下功能：

- 批量克隆 ROS Jazzy 仓库
- 批量处理 ROS 包
- 列出缺失的依赖
- 分析依赖关系（未测试）
- 自动更新 YUM 映射
- 生成 RPM 规范文件并打包源码
- 同步源码到 Gitee
- 将 Gitee 仓库设为公开
- 提取未闭环依赖

更详细的工具内容请访问[仓库](https://github.com/Sebastianhayashi/ros_openeuler_tool)

## rc_dynamics_api 构建报错分析

产出问题分析[报告](./rc_dynamics_api_report.md)

产出说明：报告中记录了我对于问题的分析，以及下一步的计划，但是还没有解决问题。