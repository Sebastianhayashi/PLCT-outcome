# 本月工作清单与简要说明

## 1. ROT 工具仓库（[链接1](https://e.gitee.com/ros-rv/repos/ros-rv/rosopeneulertool/sources)）
- **工具功能开发完成**  
  - 已开发并在本机测试完成以下功能：
    - `deploy`：部署 ROS 工具链 (rosdep, rospkg, bloom)  
    - `find-github-urls`：扫描指定目录，查找 GitHub 相关链接（排除 README）  
    - `gather-packages`：递归扫描根目录，查找 `package.xml` 并生成 `packages.json`  
    - `make-public`：批量将已存在的 Gitee 仓库设为公开  
    - `process-from-json`：从 JSON 文件批量处理包（调用 `process_packages`）  
    - `sync-gitee`：将源码推送到 Gitee 仓库  
- **当前状态**  
  - 工具已在自己电脑环境下完成功能开发与初步测试，但尚未在其他机器上进行测试。  
  - 计划后续在服务器环境模拟真实用户场景进行进一步测试。  

## 2. ROSCrossport 工具仓库（[链接2](https://e.gitee.com/ros-rv/repos/ros-rv/ros-crossport-script)）
- **功能概述**  
  - 用于将 openEuler 上的软件包生成 rosdep 能够识别的映射列表。
- **当前状态**  
  - 功能尚不成熟，测试后发现一些问题，仍需进一步完善。  
  - 优先度相对较低，后续视情况再继续开发与测试。  

## 3. 知识库（[链接3](https://e.gitee.com/ros-rv/docs?directory=0&page=1&program_id=0&scope=root)） 
  - **ROT 批量生成 spec 以及 tar.gz 文件**  
    - 主要说明 ROT 工具的工作与使用流程，帮助理解批量生成软件包所需的 `spec` 与 `tar.gz`。  

## 4. ROS 官方工具链原理说明（[链接4](https://e.gitee.com/ros-rv/docs/2906336/file/6607596?sub_id=13678608&scope=root)）
- **内容概述**  
  - 介绍了 ROS 官方打包后端 Buildfarm 的原理、 deb 与 rpm 打包的区别。  
  - 有助于对 ROS 生态下的打包与构建流程有更全面的理解。  

## 5. ROS 软件包半自动化构建流程（[链接5](https://e.gitee.com/ros-rv/docs/2906319/file/6607569?sub_id=13678605)）
- **内容概述**  
  - 详细解释如何使用 ROT 工具与 eulermaker 进行 ROS 软件包的打包与构建。  
  - 对半自动化的整个流程做了比较完整的梳理。  

## 6. Issue 追踪（[链接6](https://e.gitee.com/ros-rv/dashboard?issue=IBTM9Z)）
- **部分自动化流程讨论**  
  - 当前在讨论如果无法完全实现全自动化，是否可通过半自动的方式减少人工干预。  
  - 对应功能已在 ROT 仓库的 `find-github-urls` 命令中有所体现，处于开发与完善阶段。  

## 7. 其他工作事项及计划
1.步报告。  
   - 原计划将这些内容整理至公开知识库，但因学业繁忙暂未完成，计划下月继续完善并上传。  
2. **工具测试与打包进展**  
   - ROT 工具已完成基本功能，但尚需在服务器环境进行多机测试。  
   - 部分同学在测试时无法访问到所需环境，需后续协调服务器资源；并模拟真实用户使用场景进一步验证。  
   - 打包方面暂时无进一步进展，主要精力仍在文档整理和工具开发上。  
3. **明日会议准备**  
   - 主要汇报已完成的开发（ROT 功能完成）、文档更新，以及后续测试与打包的计划。  
   - 与导师/同事沟通后续服务器调配事宜，以及文献报告整理延后的情况。  

---

> **下阶段重点**  
> - 在服务器环境部署并测试 ROT 工具。  
> - 整理并公开已阅读文献的报告，完善知识库。  
> - 修复并完善 ROSCrossport 工具已有的问题。  
> - 跟进打包自动化/半自动化进程，确保整体流程尽量简化人工干预。

以上即为本月主要的工作清单与简要说明。