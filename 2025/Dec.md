# 十二月产出

## 核心结论

```
base -> rvv 的 phase_delta 显示，在 city10000_1 / city10000_3 上 Jacobian 阶段增幅约 +43.7% ~ +43.9%；总耗时增幅约 +7.35% / +10.79%；linear solver 阶段增幅约 +6.11% / +6.23%；residual 变化很小（-0.39% / +0.13%）。

关闭 GCC 自动向量化后的阶段变化：base -> novec 的 phase_delta 显示，Jacobian 增幅被压到 +15% ~ +19%（示例：city10000_1 jac_pct +18.62%、city10000_3 jac_pct +15.14%），同时 total_pct 约 +5%~+6% 量级。

RVV 相对 base 的主要百分比回退集中在 Jacobian（~+44%）而不是 residual/linear，而且禁用 GCC auto-vectorization 后 Jacobian 回退显著收敛到 +15~+19
```

所以目前情况更像是 GCC 在 RVV 目标下对 Jacobian 相关代码做了负向量化/负 SLP，而不是 RVV 依赖栈慢。

目前完成到：hybrid 去把“编译器策略”进一步落到具体 TU/热点路径。

## 具体做了什么

十二月的产出主要就是在 k1 上设计了四个对照组：

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

目前开发版中有的（数据、对比表格等），由于数据量太大关键信息已经都放进去 README，目前仅展示 hybrid 相关的实验文件夹结构，其他放不下：

```
[openeuler@oerv-bpi-f3 experiment]$ tree
.
├── hybrid_perf_delivery_20251230_143055
│   ├── config.sh
│   ├── logs
│   │   ├── LAST_OUT
│   │   ├── launch.log
│   │   └── run_all_20251230_144058.log
│   ├── meta
│   │   ├── meta_20251230_143101
│   │   │   └── system_and_env.txt
│   │   └── meta_20251230_144058
│   │       └── system_and_env.txt
│   ├── results
│   │   ├── fp_check_20251230_150524
│   │   │   └── fp_check.txt
│   │   ├── fp_check_20251230_151439
│   │   │   └── fp_check.txt
│   │   ├── perf_cg_rvv_vs_hyb_20251230_143101
│   │   │   ├── hybrid.city10000_1.cg.data
│   │   │   ├── hybrid.city10000_1.stderr
│   │   │   ├── hybrid.city10000_1.stdout
│   │   │   ├── hybrid.city10000_3.cg.data
│   │   │   ├── hybrid.city10000_3.stderr
│   │   │   ├── hybrid.city10000_3.stdout
│   │   │   ├── run.log
│   │   │   ├── rvv.city10000_1.cg.data
│   │   │   ├── rvv.city10000_1.stderr
│   │   │   ├── rvv.city10000_1.stdout
│   │   │   ├── rvv.city10000_3.cg.data
│   │   │   ├── rvv.city10000_3.stderr
│   │   │   └── rvv.city10000_3.stdout
│   │   ├── perf_cg_rvv_vs_hyb_20251230_144058
│   │   │   ├── diff.city10000_1.delta.symbol.txt
│   │   │   ├── diff.city10000_1.ratio.symbol.txt
│   │   │   ├── diff.city10000_1.rvv_vs_hybrid.ratio.symbol.txt
│   │   │   ├── diff.city10000_3.delta.symbol.txt
│   │   │   ├── diff.city10000_3.ratio.symbol.txt
│   │   │   ├── diff.log
│   │   │   ├── hybrid.city10000_1.cg.data
│   │   │   ├── hybrid.city10000_1.cg.report.txt
│   │   │   ├── hybrid.city10000_1.stderr
│   │   │   ├── hybrid.city10000_1.stdout
│   │   │   ├── hybrid.city10000_3.cg.data
│   │   │   ├── hybrid.city10000_3.cg.report.txt
│   │   │   ├── hybrid.city10000_3.stderr
│   │   │   ├── hybrid.city10000_3.stdout
│   │   │   ├── key.city10000_1.delta.snippet.txt
│   │   │   ├── key.city10000_3.delta.snippet.txt
│   │   │   ├── report.hybrid.city10000_3.callee.txt
│   │   │   ├── report.log
│   │   │   ├── report.rvv.city10000_3.callee.txt
│   │   │   ├── run.log
│   │   │   ├── rvv.city10000_1.cg.data
│   │   │   ├── rvv.city10000_1.cg.report.txt
│   │   │   ├── rvv.city10000_1.stderr
│   │   │   ├── rvv.city10000_1.stdout
│   │   │   ├── rvv.city10000_3.cg.data
│   │   │   ├── rvv.city10000_3.cg.report.txt
│   │   │   ├── rvv.city10000_3.stderr
│   │   │   └── rvv.city10000_3.stdout
│   │   └── perf_fp_smoke_20251230_152108
│   │       └── report.txt
│   ├── run_all.sh
│   └── scripts
│       ├── 00_collect_meta.sh
│       ├── 00_env_sanity.sh
│       ├── 01_perf_record_cg.sh
│       ├── 02_perf_report_cg.sh
│       ├── 03_perf_diff.sh
│       ├── 04_fp_check.sh
│       ├── config.sh
│       └── env.sh
├── hybrid_repro_20251229_123210
│   ├── build
│   ├── data -> /home/openeuler/planar_pgo_datasets/datasets
│   ├── logs
│   ├── results
│   └── scripts
│       └── env.sh
├── hybrid_repro_20251229_123620
│   ├── logs
│   │   ├── hybrid.build.stdout
│   │   ├── hybrid.compile.log
│   │   ├── hybrid.link.log
│   │   └── hybrid.meta.log
│   ├── results
│   │   ├── diff
│   │   ├── perf
│   │   ├── perf_rvv_vs_hybrid_20251229_124109
│   │   │   ├── diff.city10000_1.rvv_vs_hybrid.txt
│   │   │   ├── hybrid.city10000_1.data
│   │   │   ├── hybrid.city10000_1.stderr
│   │   │   ├── hybrid.city10000_1.stdout
│   │   │   ├── hybrid.city10000_3.data
│   │   │   ├── hybrid.city10000_3.stderr
│   │   │   ├── hybrid.city10000_3.stdout
│   │   │   ├── rvv.city10000_1.data
│   │   │   ├── rvv.city10000_1.stderr
│   │   │   ├── rvv.city10000_1.stdout
│   │   │   ├── rvv.city10000_3.data
│   │   │   ├── rvv.city10000_3.stderr
│   │   │   └── rvv.city10000_3.stdout
│   │   ├── perf_rvv_vs_hybrid_20251229_125102
│   │   │   ├── diff.city10000_1.rvv_vs_hybrid.txt
│   │   │   ├── hybrid.city10000_1.data
│   │   │   ├── hybrid.city10000_1.stderr
│   │   │   ├── hybrid.city10000_1.stdout
│   │   │   ├── hybrid.city10000_3.data
│   │   │   ├── hybrid.city10000_3.stderr
│   │   │   ├── hybrid.city10000_3.stdout
│   │   │   ├── rvv.city10000_1.data
│   │   │   ├── rvv.city10000_1.stderr
│   │   │   ├── rvv.city10000_1.stdout
│   │   │   ├── rvv.city10000_3.data
│   │   │   ├── rvv.city10000_3.stderr
│   │   │   └── rvv.city10000_3.stdout
│   │   └── perf_rvv_vs_hybrid_20251229_133356
│   │       ├── diff.city10000_1.rvv_vs_hybrid.symbol.txt
│   │       ├── diff.city10000_1.rvv_vs_hybrid.txt
│   │       ├── diff.city10000_3.rvv_vs_hybrid.symbol.txt
│   │       ├── hybrid.city10000_1.data
│   │       ├── hybrid.city10000_1.stderr
│   │       ├── hybrid.city10000_1.stdout
│   │       ├── hybrid.city10000_3.data
│   │       ├── hybrid.city10000_3.stderr
│   │       ├── hybrid.city10000_3.stdout
│   │       ├── rvv.city10000_1.data
│   │       ├── rvv.city10000_1.stderr
│   │       ├── rvv.city10000_1.stdout
│   │       ├── rvv.city10000_3.data
│   │       ├── rvv.city10000_3.stderr
│   │       └── rvv.city10000_3.stdout
│   ├── scripts
│   │   ├── build_hybrid_pose_graph.sh
│   │   └── env.sh
│   └── work
│       ├── pose_graph_2d.cc.hybrid.o
│       └── pose_graph_2d.hybrid
├── _inventory_last_path.txt
├── _inventory_scan_20251230_230210
│   ├── du.txt
│   ├── env_info.txt
│   ├── experiment_key_files.tsv
│   ├── experiment_tree.txt
│   ├── home_sh_ls.txt
│   ├── results_key_files.tsv
│   ├── results_tree.txt
│   └── snippets_head.txt
├── _inventory_scan_20251230_230212
│   ├── du.txt
│   ├── env_info.txt
│   ├── experiment_key_files.tsv
│   ├── experiment_tree.txt
│   ├── home_sh_ls.txt
│   ├── results_key_files.tsv
│   ├── results_tree.txt
│   └── snippets_head.txt
└── README.md

31 directories, 127 files
```

以及在实验过程中找到了 openEuler perf 上的问题，并且提了 [issue](https://gitee.com/src-openeuler/kernel/issues/IDGWNT?from=project-issue)

