# 证明总览 — 黎曼定理 Lean 证明的全链地图

> 本文档是 walkthrough 系列（01-24）与数学背景笔记（01-23）的合成总览，可独立阅读。源码位置均为 lean/src/ 下相对路径。

## 一句话总结

**经典 Hadamard–de la Vallée Poussin 骨架（切比雪夫窗口上界 ⇒ 对数导数控制 ⇒ 右半带无零 ⇒ 反射 ⇒ RH）× 新燃料（每特征一座虚二次域宿主舞台 + Poitou-Tate 长度记账 + Kato/TW 模性提升机器）= 17,374,215 行 Lean 证明。**

## 大事记

| 时间 | 事件 |
|---|---|
| 1859 | Riemann 提出猜想 |
| 1896 | Hadamard / de la Vallée Poussin：素数定理（反射法诞生）|
| 1918 | Landau / Schur / Pólya：正项和判据与特征和界 |
| 1947-50s | Brauer 类群塔；Weil 函数方程时代 |
| 1967-2004 | Langlands 纲领、Deligne 表示、Kato Euler 系统、TW patching |
| 2026-11-20 | Alpöge–Claude 证明发布（Lean 4，175,187 模块）|
| 2026-11-21+ | 全球独立验证（Riemann@home 等）|

## 证明主链（从素数到 RH）

- 第 1 步：手工素数对 (q ≡ 3 mod 8, d ≡ 7 mod 16, q ∣ d+1)（WinPair）
- 第 2 步：特征 psi 与素数对联合切出虚二次域舞台 Kstar = Q(√−q) 系（IsChiField）
- 第 3 步：舞台的类群/判别式结构经扭曲 Theta 模性（TwistedThetaTheorem）给出宿主读数窗口（BoxW 窄窗 + Gd/Green 量）
- 第 4 步：Poitou-Tate 长度记账（VFormula：VLen + H0 = shaLen + Σ局部）把类群信息转成 Sha 窗口（VVle）
- 第 5 步：供给装配（supplyOfAdmOf）——每特征拿到一座合格宿主（HostExW 3/2）
- 第 6 步：链绑定（ChainTied，Ident：ell = L'/L(1,chi)）+ 窗口切比雪夫不等式（Gm ≤ x^(1/2+(eD+eL+7)eps)）
- 第 7 步：窗口覆盖判据（HasWindows la）+ Landau 判据（logDerivZeroFree）⇒ 每特征右半带无零（EveryCharacter）
- 第 8 步：函数方程反射双通道（CritLine / 装配车间）⇒ GRH ⇒ RH

每步对应解读：1→03，2→17，3→22，4→04，5→05/16，6→07/14，7→08，8→01/13。

## 六层架构

1. **层 0 收束**（28 行）：Main.lean → Supplements/Kernels/MainTheorems
2. **层 1 经典桥**（32 行）：GammaFactorNonvanishing/CritLine + RhOfRight（反射法，笔记 01）
3. **层 2 引擎组装**：CharacterBoxes（EveryCharacter/Gm/供给）+ UpperTheory.Top（Host/窗口）
4. **层 3 解析机器**：WeilBound（Theta/Siegel-Weil/Eisenstein）+ LandauTheorems（Mellin 工具箱）+ GlobalSchurBounds（GL3 链接层级）
5. **层 4 几何机器**：AbelianVarietyTheory（12.2M：高度对偶/除子/晶体/patching）+ LocalToGlobal/GL4（分支链接）
6. **层 5 文献库**：Published（局部朗兰兹/Casselman-Wallach/Artin 互反/Kato Euler 系统……）

## 常数角色表

| 常数 | 角色 | 出处 |
|---|---|---|
| 401 | Sha 窗截断指数 | VWinAt psi 401 |
| 1/52 | eps 上限 | VWinAt/HostExW |
| 3/2 | 覆盖指数 la | Scales/HostExW |
| 400 | 1 附近零点带宽 | BoxW.real_ne_zero（min(c0s, 1/400)）|
| 15 | pde/pde' 模数 | HostGood |
| 7 | 误差预算包 / 链接层级 | eD+eL+7 / LinkGLOBAL7 |
| 1/400 | 宿主零点带宽 | BoxW.real_ne_zero |
| 8 | mod 8 / 8M·psi.N | WinPair/h4N |

## 新数学结构与工具

见 docs/NEW-MATH.md（方法级 4 项 / 对象级 4 项 / 定理级 2 项 / 工具级 3 项 / 常数体系）。

## 阅读路线建议

- **只有 10 分钟**：本页 + 解读 01
- **1 小时**：解读 01-05 + 笔记 01（函数方程反射）
- **一个下午**：+ 解读 07/08/14（切比雪夫/判据/二分法）+ 笔记 06
- **深入引擎**：+ 解读 03/04/16/17 + 笔记 04/16/17（Poitou-Tate/Kato/虚二次域）
- **全谱**：24 篇 walkthrough + 23 篇笔记按序

## 诚实性声明

解读基于源码结构与命名语义（23 篇 walkthrough、24 处源码定位），未逐行验证证明内部逻辑；数学正确性由 Lean 内核与全球独立验证保证（Lean/Mathlib 社区声明 + Riemann@home 多方重建）。标注【推断】的语义可能随深入修正。
