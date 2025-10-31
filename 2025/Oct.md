## 十月产出

## eigen

本月解决了一些上个月遗留下来的问题，如编译器向量长度固定问题等，现在可以复现测试过程，且进一步考虑对比不同编译器的加速效果：
产出文档：https://github.com/Sebastianhayashi/eigen_test

下一步计划：

等顾嘉琪的开发板架好了开始测不同板子的加速性能差异。

## ROS Jazzy openEuler

本月的工作主要是在先前工作基础上做减法，目前的工作流对比先前更加的稳定、可靠且精简。
产出了新的脚本以及文档：
- 脚本：https://github.com/Sebastianhayashi/ROS-Porting/tree/main/openEuler_Jazzy/tools

- 文档；https://github.com/Sebastianhayashi/ROS-Porting/blob/main/openEuler_Jazzy/README.md

脚本说明：

```
➜  tools git:(main) ✗ tree
.
├── gitee_bulk_delete.py -> 批量删除仓库
├── gitee_make_public.py -> 批量仓库公开
├── spilt.py -> 生成 orig 
├── stage.py -> 生成 spec
└── upload_repos.py -> 批量上传仓库

1 directory, 5 files
```

## ROS Jazzy openKylin

本月产出：

- openkylin 2.0 sp2 riscv qcow2 
- 启动 openkylin 2.0 sp2 riscv 小乌龟
- 启动 openkylin 2.0 sp2 aarch64 小乌龟

文档：
- [用 openKylin 构建 RISC-V 的 qcow2 镜像（可在 QEMU 启动）](https://github.com/Sebastianhayashi/ROS-Porting/blob/main/openKylin_Jazzy/Create_qcow2.md)
- [openKylin 2.0 SP1 上用 colcon 验证 ROS 2 Jazzy Desktop 构建——环境准备与操作手册](https://github.com/Sebastianhayashi/ROS-Porting/blob/main/openKylin_Jazzy/README.md)

镜像产出说明：

```
➜  openkylin-bundle tree
.
├── Image -> 内核
├── openKylin-Embedded-V2.0-SP2-Release-RuyiBook-riscv64.qcow2 -> 镜像
├── ROOT_UUID -> 系统 uuid
├── run-openkylin-desktop.sh -> 启动脚本（带桌面）
└── run-openkylin.sh -> 启动脚本

1 directory, 5 files
➜  openkylin-bundle
```

目前可以通过 run-openkylin.sh 直接启动镜像，但是没有桌面。

带桌面的镜像现在还在开发中。