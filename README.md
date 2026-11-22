# RiemannTheoremExploration — 黎曼定理 Lean 证明业余探索

> 2026-11-20，Anthropic 数学家 [Levent Alpöge](https://alpo.ge) 与 Claude 合作证明了黎曼猜想（含广义黎曼猜想 GRH），并以 Lean 4 形式化发布。证明已通过 Lean/Mathlib 社区与全球多方独立编译验证。
>
> 因猜想已被证明，本项目遵用户约定：**一律称「黎曼定理」**。

## 项目目标

Clone 官方 Lean 证明档案，**合作解析、理解与阅读**这份 17.37M 行的人类/AI 合作证明。明确不做本地完整编译验证（Riemann@home 已有全球多人独立验证通过）。

## 官方档案元数据

| 项 | 值 |
|---|---|
| 档案 | lean.tar.gz，239,275,554 字节（约 239 MB），14 分片下载 |
| 下载地址 | https://alpo.ge/lean.tar.gz.part01 ~ part14（按序拼接） |
| sha256 | 9631b4f020199e580ba86178cb56c6e9b09f690c2369a80dc4334aa93f49c7fc |
| 内容 | 175,187 个 Lean 模块 / 约 17.37M 行 |
| 工具链 | leanprover/lean4:v4.33.1（钉死） |
| Mathlib | 0df444a360eaa60ab8c11dca51a86af692955474（钉死） |
| 依赖公理 | 仅 Lean 三标准公理：propext、Classical.choice、Quot.sound |
| 证明范围 | 黎曼猜想 + 广义黎曼猜想（GRH）+ Dirichlet GRH |

## 目录结构

- download/ — 分片与合并后的 lean.tar.gz（git 忽略）
- lean/ — 解压后的证明源码（git 忽略，外部资产）
- docs/ — 项目文档（入库）
- docs/vibe-coding/ — 工作流记录（交互/决策/经验/调试）

## 阅读辅助生态（社区 3 日内涌现）

- [riemann-at-home](https://github.com/riemann-at-home/riemann-at-home) — 分布式验证组织与官方下载/校验流程出处
- [nasqret/riemann-rev](https://github.com/nasqret/riemann-rev) — 验证状态仪表盘与证明路线图（48 星）
- [dial481/riemann-hypothesis-rosetta](https://github.com/dial481/riemann-hypothesis-rosetta) — 200 个核心模块结构地图、导入图、阅读入口
- [tanclary/riemann-blueprint](https://github.com/tanclary/riemann-blueprint) — 证明缩减实验（-46.6% LOC）
- [lyz4tc/rh-proof-notes](https://github.com/lyz4tc/rh-proof-notes) — 逐步重建笔记

## 致谢

- Levent Alpöge（Harvard SoF / Anthropic）与 Anthropic —— 证明与其开源发布
- Lean 与 Mathlib 社区 —— 证明基础设施与验证认证
- [riemann-at-home](https://riemann-at-home.github.io/riemann-at-home/) —— 验证组织与档案元数据出处
- [Scientific American 报道](https://www.scientificamerican.com/article/anthropic-mathematician-claims-to-prove-riemann-hypothesis-most-famous-problem-in-all-of-math/) —— 新闻背景

## AI使用声明

本项目由Larkycat使用Deepseek Harness + glm-5.3-flash探索性地尝试解读，不保证任何正确性。其中使用了约2k tokens的自用全局提示词。

## 人类声明

我只是一个普通的大学生，没有足够的能力理解和验证这份探索，尝试让AI探索这个项目并尝试向我解读，仅仅是因为好奇和好玩。

这份探索不一定对，但我还是public出来了，万一对大家有什么帮助呢。

另外，最前沿的进展可以通过开源的lean代码下载到我一个普普通通的学生手上供我随意探索，这种感觉也很棒。开源万岁。