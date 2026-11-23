# 解读 29 — Greenberg-Wiles 平衡式全形与 At 八推论

> 对应第二十九轮侦察（轻量轮）。两处收口。

## 1. GreenbergWilesAt 平衡式完整形式（GalCoh.lean:175-190）

card(Sel(rho, L)) · card(H0(twDual mu rho)) · (对 v in S 求积) card(H0(rho|v)) · archH0Card
= card(Sel(twDual mu rho, perpCond(L))) · card(H0(rho)) · (对 v in S 求积) card(L v)

- perpCond(muS, rhoS, locFam, hrho.comp' 系列, L)：局部条件 L 的**正交对偶条件包**（每个 L v 给出对偶侧的对应条件）
- archH0Card：实位（阿基米德）H0 因子
- 平衡式两侧 = 同一示性数的两种记账：**正侧（rho 的 Selmer × 对偶全局 H0 × 局部 H0 积 × 实位）= 负侧（对偶 Selmer × 全局 H0 × 局部条件积）**

另确认 Universal 版公理包：LocalFiniteness / LocalTateDuality 定义为对一切 (F, Omega, l, r, M, A, rho, v) 全称量化——与解读 04 的 Statement.lean 全称风格一致（引擎侧与 CohP 侧之外的第三份：ReciprocityTheory/Hypotheses/GalCoh 侧）。**PT 假设共四份正式化**（引擎/CohP/文献/PT 假设区）。

## 2. GL3Theta 的 At 八推论结构（107-158 行）

At D cc delta g（曲线理想 + 判别式根 + 形式群绑定）推出八条性质定理（125/130/136/142/149/154/158 行各一条）——**形式群绑定的每条 Theta 构造性质都是独立推论**。这是"绑定一次，处处使用"的设计：At 成立后，Theta 级数构造的全部下游性质按需取用。

## 3. 本轮结论

Greenberg-Wiles 公式全形已录；At 八推论结构确认 GL3Theta 的"谓词-推论"组织法（与 ZetaZeroFreeRegion 的 Reads 体系一致）。

## 下一步侦察队列（边角持续）

- [ ] GL3Theta 中段 Theta 级数构造的具体定理（At 八推论的内容细节）
- [ ] LinkGLOBALPk 的 FamGL 全字段
- [ ] supplyOfAdmOf 前段 import 全景

