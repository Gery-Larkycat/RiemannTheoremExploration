# 解读 11 — RhOfRight：ζ 通道的反射封口与 Schur 界目录初探

> 对应第十一轮侦察。RhOfRight 全文解读（纯经典）+ GlobalSchurBounds 词汇群定性 + 常数 7 新线索。

## 1. RhOfRight 全文解读（Formalism/GammaFactorNonvanishing/RhOfRight.lean，Mathlib 级简洁）

rh_of_right (hz : 每个 Re(s)>1/2 的非极点 s 处 zeta(s) ≠ 0) : RiemannHypothesis

证明（与 CritLine 同构的反射，但用 Mathlib 原生 riemannZeta）：

- Re(s) > 1/2：直接由 hz
- Re(s) < 1/2：函数方程 riemannZeta_one_sub 给出 zeta(s) = (2pi)^(s-1) · 2 · cos(pi(1-s)/2) · Gamma(1-s) · zeta(1-s)；
  四因子逐一排除为零：(2pi)^(1-s) 与 Gamma 非零（正实部）；cos(pi(1-s)/2) 的零点会迫使 s 为负偶数（即平凡零点，已由 htriv 排除）——这段 "cos 零点 ⟺ 平凡零点" 的对应是函数方程两侧极点/零点结构的精确体现；zeta(1-s) 由 hz 非零（Re(1-s)>1/2）
- 结论：零点全在临界线 = RH

**解读**：ζ 通道的"封口定理"与 Dirichlet 版 critLine 完全同构——同一反射骨架的两份实例（Mathlib 原生版 vs 自建 L 函数版）。hz 的供给来自 EveryCharacter 的模 1 主特征退化（LFunction_modOne_eq），故最终路径仍是 GRH 通道（解读 10 的双通道结论获源码印证）。

## 2. GlobalSchurBounds 词汇群定性（Formalism/SharpRestriction/GlobalSchurBounds/）

目录名"全局 Schur 界"（Schur 1918 特征和经典界的现代化），文件名词汇群：

- GL3Columns / GL3Theta / AdmittedWeylDimension —— **GL(3) 的列/Theta 对应/Weyl 维数**：朗兰兹 GL(3) 层机器
- Joints / JointsF / JointsL / KernelEntryData —— 接合点/核数据（链接网络的节点）
- **LinkGLOBAL7Tied4** —— "全局链接 7 绑定 4"：链接体系的层级常数 7 与 4 直接进入文件名
- **ConclusionR7abs** —— "R7 绝对结论"：第 7 层结论的绝对形式
- **FlipTwoThree** —— "2-3 翻转"：与 WinPair 的 q≡3 (mod 8)、d≡7 (mod 16) 的模 2/3 结构呼应
- FirstClaimLemmaTwoFourOfLemmaTwoThree / LemmaBSecondBranch —— 论断 2.4 由 2.3（编号化引理链——AI 论证的组织风格）

**初步定性**：GlobalSchurBounds = 以 GL(3) Theta/接合点网络实现的全局特征和界体系；常数 7 在此是**链接体系的层级/分支常数**（LinkGLOBAL7），而非误差余项——两处"7"（误差预算 7 与层级 7）是否同源待查 LinkGLOBAL7Tied4 本体。

## 3. 组织学补记

Formalism/SharpRestriction 子目录群（GlobalSchurBounds / GrowthBounds / InertJacobiLevels / RamificationFrobenius / LocalRingCardinality / GlobalTheoremInputs 等）构成一个"约束/界"的完整理论区——SharpRestriction（锐限制）之名与 ChebyshevInequality 平方根截断的语义一致：**这个区就是"平方根截断如何被构造出来"的图纸区**。

## 4. 悬而未决

- LinkGLOBAL7Tied4 / ConclusionR7abs 本体（7 的层级语义）
- RhOfRight 的 hz 供给链（LFunction_modOne_eq 到 EveryCharacter 的退化路径文件）
- GL3Theta 的数学内容（GL(3) Theta 提升在本证明的角色——与解读 02 的 ThirdPlaceSeries 呼应）

## 下一步侦察队列

- [ ] LinkGLOBAL7Tied4.lean 本体
- [ ] LFunction_modOne_eq 供给链
- [ ] GL3Theta / ThirdPlaceSeries 串联

