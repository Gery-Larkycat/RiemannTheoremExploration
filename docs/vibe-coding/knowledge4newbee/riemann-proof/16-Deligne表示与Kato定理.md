# 数学背景 16 — Deligne 表示与 Kato 定理：从尖形式到 Selmer 有限

> 面向零基础读者。读完你将理解"尖形式带着自己的 Galois 表示"这一现代数论的核心奇迹，以及 Selmer 有限性为什么是文献。

## 1. Deligne 的奇迹（1974）：每个尖形式自带一个表示

取权 k ≥ 2 的本征尖形式 f（自守世界的"基本粒子"：q-展开 f = Σ a_n q^n，Hecke 特征值 a_n）。Deligne 证明了：

**存在二维 Galois 表示 V_f : Gal(Q̄/Q) → GL₂(系数域)，使对每个素数 p，V_f 的 Frobenius 元的特征多项式恰为 x² − a_p x + p^(k−1)**

即：**自守侧的数值（a_p）与算术侧的对象（Galois 表示）精确对应**。这是朗兰兹纲领 GL(2) 情形的定理化（此前只是 Eichler-Shimura 在特殊权上的观察）。

本项目 KatoLitO 的第一段（存在连续 V 满足 FrobPoly）就是这个定理。

## 2. Kato 定理：Selmer 群的有限性（2004）

把 V_f 扭转（乘分圆特征 ρ 次）并限制到 Abel 扩张 K，得到 Selmer 群（解读 04：满足局部条件的 H¹）。**Kato 定理**：在非临界 r（1 ≤ r ≤ k−1，2r ≠ k）处，这个 Selmer 群**有限**。

- **临界条件 2r ≠ k**：r = k/2 恰是"中心点"（zeta 函数的 s = 1 类比），那里 Selmer 可能无限——与 BSD 类问题接壤，是需要排除的例外
- 有限性来自 Kato 构造的 **Euler 系统**：一族用特殊值显式构造的上同调类，其局部化公式给出 Selmer 的"消化上界"

## 3. 文献供"有限"，引擎供"多少"

本项目对 Selmer/Sha 的需求分两层：

1. **有限性**（shaLen ≠ ⊤）：Kato 定理（文献级，LiteratureResults 接入）
2. **数值界**（shaLen 的指数和 ≤ e^(x^eps/2)）：引擎自己的窗口估计（新数学所在）

这个分工在架构上很聪明：**可靠的部分用文献，新颖的部分自己证**——AI 证明的"保守性设计"。

## 4. TW 障碍界与 Greenberg-Wiles

- Taylor-Wiles 拼贴的每一步需要"提升剩余表示且保持注入有限"（Ramakrishna 型引理）——本项目 Norm 定义即其形式化
- **Greenberg-Wiles 公式**：带局部条件 Selmer 群的 Euler 示性数公式（Poitou-Tate 的条件版精化）——CohP 结构体的 gw 字段

## 术语速查

| 术语 | 一句话 |
|---|---|
| 本征尖形式 | 自守世界的基本粒子（Hecke 特征向量）|
| Deligne 表示 | 尖形式自带的二维 Galois 表示 |
| Kato 定理 | 非临界扭转 Selmer 群有限 |
| Euler 系统 | 相容上同调类族，给出消化上界 |
| 临界指数 | 2r = k 的中心点（例外位置）|
| Greenberg-Wiles | 条件 Selmer 的 Euler 示性数公式 |
| Hida 族 | 沿权方向连续变形的尖形式族 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| KatoLitO 的 ∃ V 连续 ∧ FrobPoly | Deligne 表示 |
| SelAll (...) .Finite | Kato 有限性 |
| 2 * r ≠ k | 临界指数排除 |
| CohP 的 gw 字段 | Greenberg-Wiles 公式 |
| Norm 命题 | TW 提升障碍界 |
| HidaSetting | Hida 族框架 |
