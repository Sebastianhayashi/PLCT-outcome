# 九月产出

## OBS 使用文档

1. 如何使用 OBS 网页端 -> https://github.com/Sebastianhayashi/ROS-Porting/blob/main/Building_platform/Create%20_project_on_OBS.md
2. 如何使用 OBS 命令行 -> https://github.com/Sebastianhayashi/ROS-Porting/blob/main/Building_platform/OBS_Cli.md

## openEuler 24.03 LTS ROS Jazzy 移植

前半个月的工作主要是在对其与韩老师那边的规范，但是他们的规范在变动且没有定数所以我也在动态的调整我的规范。后半个月的工作主要是在往官方规范外加精简工作流的方向重新调整规范以及脚本工具。

主要调整调整内容为：将 spec 中的多余的补丁使用构建工具如 eulermaker 自身去实现，给 spec 打极小补丁以适应 openeuler。

同时在将整个构建流程撰写成文档。这么做的好处是在于后续为 openEuler ROS 做贡献的人可以更加简单高效的去复用这个工作流，提供一个与 openEuler 社区不同的思路参考。

文档：

脚本：

## eigen 库测试对比

按照顾嘉祺的[文档](https://note.cd.al/zh-CN/notes/Operating%20System/rvv-benchmark/eigen3-riscv-rvv1-benchmark.html)中的内容，该测试聚焦于对比 eigen 库在启用了 RVV 加速补丁以及官方无补丁版本两者跑 bench 测试的性能差距。

官方版可以正确构建 bench/btl 下的所有的测试，但是 RVV 加速版本只能构建四个基准测试，即使是基准测试的情况下也相对耗时（四个测试至少需要四个小时）。

前半个月的工作主要是在查询各种文档以及根据编译器的错误调整测试的方案，后半个月的工作是在对比两者之间四个基准测试的性能差异，并且产出 means 图作为对比，更详细的内容参见这里。

## openkylin 打包


