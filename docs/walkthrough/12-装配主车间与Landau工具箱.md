# 解读 12 — 装配主车间、Landau 工具箱与 GL4 分支链接

> 对应第十二轮侦察。三个大件定名：装配主车间（RiemannHypothesisOfEveryCharacter）、Landau 工具箱（LandauTheorems 36 文件）、GL4 分支链接（BranchingLinkFamily）。

## 1. 装配主车间：RiemannHypothesisOfEveryCharacter.lean（231 行）

文件名即使命题：**从 EveryCharacter 推出 RH**——解读 01 的 rhOfAll 供给链的实体车间。其 imports（25+ 条）是一份巨型配料表：

- SiegelWeilUnitaryConvergent2 / ExistsNotEisContinues —— Siegel-Weil 酉收敛
- SatakeParameters.ExistsCount / HeckeLPartialContinuation —— Satake 参数与 Hecke L 延拓
- DiscreteSeriesClassification / FlagMeasures —— 离散系列分类
- PeriodComparisonOfGaussManinPeriods —— Gauss-Manin 周期比较
- **SiegelKlingenDeligneRibetOfBoth** —— **Siegel–Klingen–Deligne–Ribet 定理群**（L 函数临界值的著名特殊值理论）
- EisensteinSeriesContinuationModuli / IwasawaDecompositionUnitary / CuspTraceClassOfFactorisation —— Eisenstein 延拓、岩泽分解、尖形式迹类
- CrystallineDeRhamAbelianStructureOfStatements —— 晶体 de Rham 结构

第 213 行使用 LFunction_modOne_eq（模 1 退化）—— rh_of_right 的 hz 供给链入口确认。**这份 import 清单本身就是"证明用了哪些数学"的权威清单**，比任何二手总结都可靠。

## 2. Landau 工具箱：LandauTheorems 36 文件（DedekindLFunctions/）

ChBalance / ChCore / ChTop（特征三件套）、GchiGrowth / GchiConj（Gchi 增长与共轭）、**LandauCauchy / LandauCoeff / LandauDichotomy / LandauFinite / LandauGrowthContra / LandauKernelMax / LandauNearest / LandauPoleAsym / LandauPoleReLe**（Landau 九件套：Cauchy 框架、系数、二分法、有限性、增长反证、核最大、最近点、极点渐近与实部上界）、CharFamilyLFunctionNeZeroOfOneLeRe（**特征族 L 在 Re≥1 无零**——主项判据的族版）、MellinRamp / WindowHypOfRpow（Mellin 斜坡与窗口假设）。

**解读**：Landau 路线（解读 07-08 的正项和判据）在此有完整的"工具箱级"实现——从 Mellin 表示到极点渐近到二分法反证。Landau.lean（TotientGaloisClasses 侧）与 LandauTheorems（DedekindLFunctions 侧）是同一机器的两级：前者上同调侧装配，后者解析侧原语。

## 3. GL4 分支链接：BranchingLinkFamily

LinkGLOBAL7Tied4 的 imports 揭示链接体系运行在 **GL4**（GlobalTheory/GL4/）上：BranchingLinkFamilyNormalised / BranchingIntegralNormalised / ColumnLatticeExactSlope / ClassMapArchimedean……

- **Branching（分支）**：GL4 列结构上的分支链接族（归一化）——解读 11 的"链接层级 7/4"现在有了坐标：全局链接 GLOBAL 系列在 GL4 分支族上编号（7 = 全局层级，4 = 绑定层级）
- GL3Theta/GL3Columns（解读 11）与 GL4 分支：多层 GL(n) 结构并存——与 Theta 提升的梯子（GL2×GL2→GL4、GL2→GL3）吻合

## 4. 更新后的全证明架构图（13 轮积累）

- **层 0 收束**：Main（12 行）→ MainTheorems（16 行）
- **层 1 桥**：CritLine + RhOfRight（32 行，经典反射）
- **层 2 引擎组装**：CharacterBoxes（EveryCharacter/Gm/供给链）+ UpperTheory.Top
- **层 3 解析机器**：WeilBound（Theta/Siegel-Weil/Eisenstein）+ LandauTheorems（Mellin/Landau 工具箱）+ GlobalSchurBounds（GL3/链接层级）
- **层 4 几何机器**：AbelianVarietyTheory（12.2M：高度对偶/除子/晶体/SiegelKlingenDeligneRibet）+ GL4 分支链接
- **层 5 文献**：Published（局部朗兰兹/Casselman-Wallach/Artin 互反……）

## 下一步侦察队列

- [ ] RiemannHypothesisOfEveryCharacter 213 行前后（modOne 退化细节 + 主定理陈述）
- [ ] SiegelKlingenDeligneRibetOfBoth 定理陈述（特殊值定理群的角色）
- [ ] LandauDichotomy（二分法）本体

