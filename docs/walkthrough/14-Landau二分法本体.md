# 解读 14 — Landau 二分法本体与 Level-3 临界退化

> 对应第十四轮侦察。LandauDichotomy 全文解读 + SmallClassNumbers 认知修正。

## 1. LandauDichotomy 全文解读（91 行）

定理 landau_dichotomy 的设置：Z ⊂ ℂ（如 L'/L 的极点集 = L 的零点集），假设：局部孤立性（每点邻域无其他 Z 点）、全体实部 < σ、存在实部超过 θ 的点 ρ₀。结论二分：

- **左支（真空半径）**：存在 D ≤ σ−θ，使 Z 与开球 B(σ,D) 不相交，且 Z 中存在实部 > σ−D 的点——**零点集与竖线 σ 之间有半径 D 的真空区**
- **右支（孤立实点）**：存在唯一 β ∈ Z ∩ ℝ（θ < β），某半径 r 内 Z ∩ 球 = {β}——**最近点恰是实数点**

配套原语：landau_finite（Z ∩ 闭球有限——局部孤立 + 紧性）、exists_min_image（取距 σ 最近的点）。

**数学语义**：这是经典 Landau 论证的结构化——"要么零点与参照线之间有量化真空带（得到界），要么最近的点恰在实轴上（而 exp 型正性函数在实轴上的行为可被正性单独排除）"。二分法为窗口化界提供量化半径（Window.lean:26 的反证形态 y^θ < Gm y 即基于此类真空量化）。右支的排除在引擎中由正项和的正性（Gchi ≥ 0 型量）完成。

## 2. SmallClassNumbers 认知修正（ClassNumberThree.lean，115 行）

classNumber_three : classNumber (Kstar 3) = 1

修正解读 13 的猜测：这不是数论"虚二次域类数"问题，而是**引擎自身 Level-3（层级 3）临界退化的处理**：

- Kstar 3 = 层级 3 的星型域对象，其 classNumber（该对象的分类数）= 1——**类群平凡 ⇒ 层级 3 的结构退化/简化**
- eq_one：模 2 的 Dirichlet 特征恒为主特征（模 2 特征群平凡——特征枚举在最小模处平凡化）
- vlen_one：长度量 = 1；LenEqZeroIff：长度为零的判据；bound_of (U3.CorGK) ⇒ Bound——层级 3 的界由 CorGK 条件推出

⇒ MainTheoremsCritical 的语义：**最小层级（Level 3）与最小模（mod 2）的退化情形特判**——大机器的边界兜底件（"类数"是引擎词汇表中的分类数，与虚二次域类数问题无关）。解读 13 笔记中"Heegner/类数 1 域"的类比不适用，特此修正。

## 3. 与笔记 13 的对照修正

笔记 13 的"类数 h(K)/Heegner 数"背景知识本身成立（作为数论知识），但与源码 ClassNumberThree 的对应关系应理解为"引擎 Level-3 对象的类数平凡性"。术语对照表修正：classNumber (Kstar 3) = 引擎层级 3 域的分类数。

## 4. 悬而未决（持续）

- LinkGLOBAL7 层级表（GL4 分支族的完整编号）
- Kstar 定义本体（层级 i 的星型域构造——Kstar 3 的"3"即层级号）
- supplyOfAdmOf 证明体中部（40 行之后的策略组合）
- GL3Theta ↔ GL4 梯子抽样

## 下一步侦察队列

- [ ] Kstar 定义本体
- [ ] CorGK / U3 语义（层级 3 的界条件）
- [ ] LandauTheorems/LandauFinite 与 landau_finite 的关系

