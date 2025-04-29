# 四月产出

**一句话说明**：本月核心产出主要是成功解决了 rosdep 的核心依赖文件，使用 ament 系列包跑通整个构建流程，开始着手撰写相关文档。

## rosdep 依赖维护

> 完成维护 rosdep key 工作核心工作流

说明：这个月能够使用自动化脚本生成 rosdep 的依赖清单（.yaml），详细内容可以参考文档。
产出脚本：

- [fetch_src_deps.py](https://gitee.com/ros-rv/scripts/raw/master/fetch_src_deps.py)
- [enerate_openeuler_rosdep.py](https://gitee.com/ros-rv/scripts/raw/master/generate_openeuler_rosdep.py)

目前使用 eulermaker 构建软件包的几个痛点（工作里程碑）：

- [x] rosdep 不支持 openeuler 条目
  - 上述工作已经解决该问题，后续会根据不同的包持续更新 [.yaml](https://gitee.com/microseyuyu/oe_jazzy_docs/tree/master/Lists/rosdep)
- [ ] GitHub 链接无法下载
  - 正在搜集相关包，已经整理成清单（准备更新）
- [ ] 特殊包问题
  - 有些包如 `rti-connext-dds-cmake-module` 等存在特殊的中间件问题等特殊情况

### 其他说明

GitHub 链接无法下载这个问题，目前的解决思路是 -> 人工维护链接列表，使用脚本自动 patch 到对应的软件包。
目前搜集了一个相关链接列表，现在在做成可以让脚本自动解析并且 patch 的 json 文件，预计这个列表会随着对应的脚本一起更新。

## openEuler 缺包列表维护

说明：目前在软件包构建时候遇到系统等软件包缺失，已经开始维护成一个列表，正在做增量更新，列表请参考[这里](https://gitee.com/microseyuyu/oe_jazzy_docs/blob/master/Lists/mssing_packages.md)。

## 文档

> 工作流及其问题已经清晰，文档的大纲已经写出来了，在开始做内容增量

仓库请参考[这里](https://gitee.com/microseyuyu/oe_jazzy_docs.git)。

文档目前有的内容简要说明：
- 主要工作流
- 如何在 openEuler 上快速部署 ROT 相关环境
- 可能出现的问题以及解决办法
- 生成 `.spec` 以及软件包源码
  - 特殊包问题
  - GitHub url 问题
  - eulermaker 适配说明
- 将 ROS 官方工具链移植到第三方系统
- 维护清单
  - 缺包
  - rosdep yaml

> 以上内容属于计划内，文档目前并没有完全写完，详细参考仓库内的内容。

文档目前结构：

```
  oe_jazzy_docs git:(master) ✗ tree
.
├── Lists
│   ├── README.md
│   ├── mssing_packages.md
│   └── rosdep
│       ├── openeuler_base.yaml
│       └── openeuler_python.yaml
├── Pitfalls
│   ├── Github_url.md
│   ├── Porting.md
│   ├── README.md
│   ├── rosdep_yaml.md
│   └── spec‑adaptation‑openeuler.md
├── README.en.md
├── README.md
└── Workflow
    ├── 0_Preparation.md
    ├── 1_Generate.md
    ├── 2_Sync_Publish.md
    ├── 3_eulermaker_Project.md
    ├── README.md
    └── Workflow.md

5 directories, 17 files
```

## 源码包

> 目前在 ros-rv 仓库中已经有 60 个确定符合规范能够正确构建、使用的软件源码包。

参考[这里](https://e.gitee.com/ros-rv/projects/738428/repos)。

目前只有 ament 相关的包，接下来会一次性更新如下相关的软件源码包：

- [x] ament
- [ ] eProsima
- [ ] ros2
- [ ] ros-tooling
- [ ] eclipse-cyclonedds
- [ ] gazebo-release
- [ ] osrf
- [ ] ros-perception
- [ ] ros-visualization
- [ ] eclipse-iceoryx
- [ ] ros
- [ ] ros-planning

说明：一开始拿 ament 系列的包来测试整个工作流，现在确定工作流稳定，现在只需要验证其他的包覆合规范且可以使用即可直接上传。

## PPT

PPT 内容整理

> 群内紧急任务
