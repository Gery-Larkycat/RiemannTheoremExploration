# 解读 07 — 平方根截断与 Landau 判据：零点自由的最后一公里

> 对应第七轮侦察。引擎的核心不等式与零点自由判据全部现形。

## 1. 核心不等式：平方根截断（TopDefs.lean:26）

ChebyshevInequalityForFamily / OnWindows 的结论均为：

**存在 x1，凡 x ≥ x1：Λ.Gm x ≤ x^(1/2 + (eD + eL + 7)·eps)**

Gm 是特征层级 Λ 的核心求和量；不等式说它的增长达到**平方根级别加可任意小的余项**（eps 可趋于 0）。平方根截断正是 GRH 的等价语言（GRH ⟺ 素数/特征和的误差为平方根级）。

组件语义链（TopWin.lean）：

- ChebyshevInequalityOnFamilyWindows：窗口族上每点链绑定 Tied 成立（常数 K cHH eK CL x0 存在）
- ChebyshevInequalityAtWindowScale la Λ：存在 eps<ε₁ 的窗口族，兼具 EFamC（特征循环存在）+ Windows la + 链绑定
- TiedAll：WinAll 版（覆盖一切大 x）
- tiedWin_of_ex：**ExWin（存在合格窗口族，含 HypV 形状假设）+ ChainWin（链式传递绑定）⇒ AtWindowScale**——放大器的组合引理

## 2. Landau.lean：零点自由判据层（592 行）

两个关键定理片段：

1. **logDerivZeroFree**：设 P 满足微分方程 P' = q·P（q 为正值函数）且 P 在区域某点非零，则 P 在整个区域无零点。—— 这是 **Landau 型零点判据**（正实部指数型函数无零点，源自 exp 的正性）。引擎用它从"实部恒正"推"P 无零点"。
2. **re_gChi**：对非主特征 ξ，复值量 An.gChi ξ y 的实部 = Gchi ξ y（正项和）。展开涉及 sumLamChi（**von Mangoldt 函数 Λ(n) 加权求和**）与 log(y/n) 因子——**这正是 Landau 1918 年技巧**：y^s 相关的积分把 L'/L(s,χ) 变成 Σ Λ(n)χ(n)·log(y/n)/n 的正项级数。

⇒ 引擎的零点自由论证范式：**正项和（Gchi/Gm）的平方根截断 ⇒ 指数型量的实部控制 ⇒（Landau 判据）⇒ 零点自由**。

## 3. Level 层的真身：InertJacobiLevels

Formalism/SharpRestriction/InertJacobiLevels/（48 个文件）文件名群即语义：

- TwoPrimeFieldMemLevelOfCoprime / TwoPrimeFieldSatisfiesConditions —— **两素数域（WinPair 的 q,d）属于层级**：层级由互素素数对生成
- PrimeSupply / RayPrimes / GenSplit —— 素数供给与射线分裂
- Inert / Jacobi —— 惯性类与 Jacobi 符号（二次特征）
- TiesAtY / TiesCore / TiesAsm / TiesLat —— 各尺度绑定
- HostFam —— 宿主族
- VVEqEmptyOfNotIsResidueClassZero —— VV 非退化条件

⇒ **Level = 由互素素数对（q,d）+ Jacobi 惯性类刻画的特征层级**；解读 03 的 WinPair 正是 Level 的入口数据。

## 4. 引擎全景（终版快照）

- 素数对 (q,d) → Level（两素域 + Jacobi 惯性）→ 宿主 E（五素数仪表盘 + 范数方程）
- E 的 LData → Poitou-Tate 长度记账（VFormula）→ Sha 窗口（VVle，401 截断）
- 窗口 → 链绑定（ChainTied，Ident：ell = L'/L(1,χ)）→ 切比雪夫不等式（Gm 平方根截断）
- →（Landau 判据）零点自由 → EveryCharacter → VW 桥 → RH

每一步都是"上一层的输出即下一层的输入"，全链无断点。

## 5. 剩余未知（优先级排序）

1. Gm 的精确定义（哪个求和量）——Level 字段，待挖 Landau.lean 前段
2. LChain（LFunctionChainParameters）——链的代数定义
3. supplyOfAdm 实例化细节（VWinAt ⇒ HostExW 的构造步骤）
4. GlobalInterpolation Link 网络（TopG/FamilyClassConnected）
5. 常数 7 的出处（eD + eL + 7 中的 7）

## 下一步侦察队列

- [ ] Gm 定义（Landau.lean 前段/Level 定义文件）
- [ ] LChain 定义
- [ ] ExplicitFormulaError 本体（显式公式误差）
- [ ] supplyOfAdm 构造

