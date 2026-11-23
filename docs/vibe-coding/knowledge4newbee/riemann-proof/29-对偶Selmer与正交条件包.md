# 数学背景 29 — 对偶 Selmer 与正交条件包

> 面向零基础读者。读完你将理解 Greenberg-Wiles 平衡式的完整形态，以及"对偶条件"为什么是条件包的镜像。

## 1. 平衡式全形

一侧：card(Sel(rho, L)) · card(H0(rho*)) · Π局部 card(H0(rho|v)) · 实位因子

另一侧：card(Sel(rho*, L⊥)) · card(H0(rho)) · Π局部 card(L v)

其中 rho* = 对偶扭转表示，L⊥（源码 perpCond）= 局部条件包 L 的正交对偶。

**读法**：Selmer(ρ, L) 的大小被三件事定价——对偶 Selmer 的大小、全局 H0、以及"每个局部条件有多宽"（Π card(L v)）。条件越宽（L v 越大），Selmer 越大，但对偶侧越小——**守恒**。

## 2. 正交条件包 perpCond

每个局部条件子模块 L v ⊂ H¹(ρ|v) 有它的正交伴随 L⊥v ⊂ H¹(ρ*|v)（经局部 Tate 配对）。Greenberg-Wiles 使用的是"L 的正交包"作为对偶侧条件——**条件的镜像**。

直觉：如果说 Selmer(ρ, L) 是"满足约束的解"，Selmer(ρ*, L⊥) 是"约束的对偶侧解"；两者大小满足刚性平衡，无法同时膨胀。

## 3. 四份 PT 正式化的分工（更新）

1. Formalism/GaloisCohomology/Statement.lean——引擎侧假设包（四条 PT 假设 + VFormula）
2. CohP 结构体（PatchingModules）——TW 侧性质包
3. Published.PoitouTateNormalised——文献侧
4. ReciprocityTheory/Hypotheses/GalCoh——PT 假设区（LocalFiniteness/LocalTateDuality 全称包 + GreenbergWilesAt 本体）

**四份各有分工**：引擎侧供 VFormula、TW 侧供 patching、文献侧供认证、PT 假设区供平衡式。同一数学、四种粒度——多级接入设计的极致案例。

## 4. At 八推论：谓词-推论组织法

GL3Theta 的 At（绑定谓词）带八条推论——"绑定一次，处处使用"。这是解读 16 CohP/解读 26 tVol-t10 条件清单的同款组织法：**把大前提打包成一个谓词，推论按需展开**。对读者的导航价值：找到谓词定义，就找到了全部下游推论的公共前提。

## 术语速查

| 术语 | 一句话 |
|---|---|
| 对偶 Selmer | 对偶扭转表示上的正交条件 Selmer |
| perpCond | 局部条件的正交对偶包 |
| arch 因子 | 实位（阿基米德）贡献 |
| At 谓词 | 形式群绑定条件，八推论的公共前提 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| perpCond muS rhoS … L | 正交对偶条件包 |
| archH0Card | 实位 H0 因子 |
| LocalFiniteness/LocalTateDuality（Universal 版）| 全称公理包 |
| At 的八条 ∀ 推论 | 谓词-推论组织法 |
