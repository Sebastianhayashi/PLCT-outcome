# 十二月产出

十二月的产出主要就是在 k1 上做了四个 ceres 相关的实验：

- base（基线）：不走 RVV 目标/路径，作为“标量路径 + 常规优化”的性能基线（也就是官方版，作为对照）
- rvv：启用 RVV 生态（目标 ISA/库路径），观察“开启 RVV 后端到端”的整体收益或退化（也就是 RVV 版）
- novec：在 RVV 生态，但通过 -fno-tree-vectorize（以及常配套的 SLP 关闭）来关掉 GCC auto-vectorization，用于验证“退化是否主要来自编译器自动向量化负优化”
- hybrid：保持 build-rvv 的依赖/静态库/链接方式不变，只对 一个 TU（pose_graph_2d.cc） 追加 -fno-tree-vectorize -fno-tree-slp-vectorize 重编并重新链接，得到新二进制——本质是“RVV build + 单 TU 禁向量化”

做了三组实验：

1. base vs rvv：rvv 相对 base 存在明显变慢的情况，为了更进一步的找出哪里拖累性能衍生了下面的实验。
2. rvv vs novec：如果 novec 相对 rvv 明显回升（或退化显著缓解），可以基本锁定：问题核心在 编译器自动向量化策略（而不是 RVV 依赖栈本身）。
3. rvv vs hybrid：hybrid 实验的价值在于把根因定位从“编译器整体策略”进一步收敛到“具体 TU/具体热点代码路径”。

但是目前 hybrid 卡在了 perf 无法做 call-graph dwarf。

目前仓库中有的内容：


```
Ceres_optimization git:(main) tree
.
├── README.md
├── eigen_rvv_check.cc
├── results
│   └── Perf_city_1
│       ├── base.city10000_1.report.txt
│       ├── base.city10000_3.report.txt
│       ├── diff.city10000_1.txt
│       ├── diff.city10000_3.txt
│       ├── rvv.city10000_1.report.txt
│       └── rvv.city10000_3.report.txt
└── tools
    ├── sweep_base.sh
    ├── sweep_hybrid.sh
    └── sweep_rvv.sh

4 directories, 11 files
```

三个核心脚本，同时 README 中详细讲述了目前的情况。

以及在实验过程中找到了 openEuler perf 上的问题，并且提了 [issue](https://gitee.com/src-openeuler/kernel/issues/IDGWNT?from=project-issue)

