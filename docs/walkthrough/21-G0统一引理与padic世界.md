# 解读 21 — G0 统一引理、ζ 通道适配层与 p-adic 幂级数世界

> 对应第二十一轮侦察（轻量轮）。三个澄清：gauss_sum_function_eq 的真身、ZetaZeroFreeRegion 的层次结构、GL3Theta 的 p-adic 世界。

## 1. gauss_sum_function_eq = G 系列统一引理

private theorem gauss_sum_function_eq (χ) (y) : An.gChi chi y = G0 chi y

内容：把 Landau 复量 An.gChi 统一改写为 **QH 侧统一 G 函数 G0**（主特征走 G1、非主走 Gchi；max(y/n−1, 0) 在支撑 n ≤ y 上退化为 y/n − 1）。名字里的 "Gauss sum function" 指 **G0 函数族**（G 系列求和函数），"Eq" 是表示统一。修正解读 18 的初步猜测（并非 Gauss 和 tau 本身的恒等式——Gauss 和机器在 thinH 的下游使用）。

配套：isReal_of_sq（chi^2 = 1 时取值实数——实特征引理，对应 WinPair 分支的 real 情形）。

## 2. ζ 通道层次结构（三层）

- GlobalSchurBounds/ZetaZeroFreeRegion —— 证明真身
- GlobalRankLatticeProofs/ZetaZeroFreeRegion（20 行薄适配层）：**G_eq_Gz（GlobalTheoryTheory.G y = Formalism.Gz y，命名空间桥接）** + points_property_of_d7（D7 数据的 PointsLemma）
- 上游（MainTheorems/条件主定理层）引用适配层

**命名空间桥接引理**（X.Y = Z 形式）是 AI 代码的常见缝合器——在解读 19-20 已见多例（An.gChi = Gchi、An.logDerivativeAtOne = logDerivativeAtOne、G_eq_Gz）。这是跨目录装配的"逻辑焊点"清单。

## 3. GL3Theta：p-adic 多元幂级数世界（1013 行）

namespace Formalism.MainNotions.GL3Theta 的基础词汇：

- Wp p：Q_p 的子环（Z_p 型）；InWf：积分点判据（p^k · x ∈ Wp）
- MvPowerSeries sigma Cp：多元幂级数（sigma 索引集）
- IntegralW / CoefWf：级数与系数的积分性
- logMv：多元 log 级数；Simeq / SimeqW：相似性（W-加权版）
- **tauK / tauKc (D) (lam : Qbar →+* Cp) (a : D.host.K)**：从代数闭包嵌入 lam 与宿主域元素 a 构造的 p-adic 量——**Gauss 和的 p-adic 化身**（tau 正是 Gauss 和的传统记号！）

⇒ GL3Theta 的数学身份：**p-adic 多元幂级数层上的 GL3 Theta 对应**——解读 02 的 Prismatic/Dieudonne 线索在此成形：引擎的 Theta 机器有复解析与 p-adic 两套（后者用于宿主域元素在 l 位的行为）。

## 4. 悬而未决（收尾清单）

- LinkGLOBAL7 的"7"完整层级表（已知 GLOBAL7/绑定 4 的坐标）
- GL3Theta ↔ GL4 梯子关系
- supplyOfAdmOf 尾部
- Gz 的 LandauZeroFreeHalfPlane 实例化路径（GlobalSchurBounds/ZetaZeroFreeRegion 真身待读）

## 下一步侦察队列

- [ ] GlobalSchurBounds/ZetaZeroFreeRegion 真身
- [ ] GL3Theta 主定理段（1013 行中的定理群）
- [ ] supplyOfAdmOf 尾部

