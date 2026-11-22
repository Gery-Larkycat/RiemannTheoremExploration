# 数学背景 24 — Greenberg-Wiles 公式：Selmer 的 Euler 示性数

> 面向零基础读者。读完你将理解"Selmer 群的大小"如何被一个精确的平衡公式定价。

## 1. Selmer 群回顾

Selmer(ρ, L) = H¹ 中满足逐位局部条件 L 的子群（解读 04）。它测量"Galois 表示 rho 的可容许扭曲解"。

## 2. Euler 示性数：加减法的艺术

对一个群链

0 → H⁰ → H¹ → H² → 0

Euler 示性数定义为"长度交替和"：len(H⁰) − len(H¹) + len(H²)。**正合性使它保持平衡**——这是 Poitou-Tate 的核心（解读 04）。

## 3. Greenberg-Wiles 公式：带条件的平衡

带局部条件 L 时，Selmer 的示性数不再平凡，但**可精确计算**：

card(Sel(ρ,L)) / card(H⁰(ρ)) = (各局部因子的乘积) / card(Sel(ρ*, L*))

（ρ* = 对偶扭转；实位贡献 arch 因子。）这就是 Greenberg-Wiles 公式：**Selmer 的大小由其对偶 Selmer 与局部因子定价**。

引擎场景（GreenbergWilesAt）：rho = 分圆扭转 twisted Dirichlet 场景，mu = 分圆特征 mod l^r，条件带实位共轭条件——**全部条件在引擎语境下可验证**（CohP 结构体逐条供给），于是 Selmer 基数公式可用。

## 4. 它如何喂饱 RH 证明

- Sha¹(ρ) = Selmer 与"全局真实解"之差（解读 04）
- Greenberg-Wiles 把 card(Sel) 与 card(Sha)、局部因子绑成一个平衡式
- Kato 有限性给 Selmer 有限（解读 16）
- 引擎的窗口估计给平衡式各因子的界
- 平衡式 ⇒ Sha 长度的界 ⇒（解读 08 的 Landau 判据）零点自由

**一条从"局部条件"直通"零点缺席"的管道**——这就是为什么"每特征一个宿主+一套局部条件"是引擎的中央设计。

## 术语速查

| 术语 | 一句话 |
|---|---|
| Euler 示性数 | 长度交替和，正合链的不变量 |
| Greenberg-Wiles | 条件 Selmer 的示性数平衡公式 |
| twDual | 对偶扭转表示 |
| LocCond | 逐位局部条件包 |
| arch 因子 | 实位（阿基米德）因子 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| GreenbergWilesAt | 平衡公式本体 |
| 前提 card Sha1 = card Sha2 | PTShaAt（解读 04）|
| LocCond / archH0Card | 局部条件包 / 实位因子 |
| supplyOfAdmOf 的 hprime/hbd | 宿主素因子限制与有界扭转 |
