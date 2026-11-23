# 数学背景 34 — Weil 表示的相位与 2-上循环

> 面向零基础读者。读完你将理解 Weil 表示为什么是"投影表示"、(−1)^m 相位从哪来、以及"上循环"是什么。

## 1. Weil 表示：辛群的线性化身（带一个瑕疵）

解读 02 介绍过：Weil 表示把辛群（Theta 级数的对称群）表现为 Schwartz 空间上的算子。但严格的构造有个著名的**小瑕疵**：

W(g)·W(h) ≠ W(g·h)，而是 = c(g,h)·W(g·h)

修正因子 c(g,h)（2-上循环/cocycle）不为 1——**Weil 表示是投影表示**（projective representation）。c² = 1 型的符号因子（本引擎 kap）正是投影障碍。

## 2. (−1)^m 相位：Gauss 和的符号

Weil 相位函数 wPh 在 p-adic 逼近点上的取值公式（本引擎 wPhase）：

若 p^k · qH(x) = m（qH 是二次型，m 是整数），则 wPh(p, x) = (−1)^m

这来自**二次 Gauss 和的经典计算**：Gauss 和 tau(a) = Σ exp(2πi a n²/q) 的符号由 a mod 4/8 决定。**这就是为什么引擎的素数对要求 q ≡ 3 (mod 8)、d ≡ 7 (mod 16)**——钉死 Gauss 和的符号歧义，让相位因子完全可预测！

## 3. 上循环：非交换性的账本

W(g)W(h) 与 W(gh) 的差 c(g,h) 满足**上循环恒等式**（c 在三元组合中自消）——它不是 bug 而是 feature：投影表示的"c"携带了表示无法线性化的部分对称信息。**kap = c 的显式形式**（本引擎 wCocycle）。

处理投影表示的标准手法：把 c 吸收进中心延拓（Steinberg/ metavariable 群）或在关键处用 c² = 1 的特殊性消去——引擎走的是第二条路（素数条件钉死符号）。

## 4. 换格公式：sqrt 缩放律

Theta 级数随格 L 变化的缩放因子 = 格指标比的开方：

Theta 在格 L' 的值 ≈ sqrt(vol(L,L')) 因子 × 换格算子作用于 L 的值

（vol = 双向指标比。）直觉：**格变密 Theta 变小，且恰好是体积比的平方根**——这是"解析对象与几何对象的平方根对偶"，与 RH 的 1/2 指数遥相呼应。

## 术语速查

| 术语 | 一句话 |
|---|---|
| 投影表示 | 差一个标量因子的表示 |
| 2-上循环 | 表示复合的修正因子 c |
| Weil 相位 | Gauss 和的符号 (−1)^m |
| 换格公式 | Theta 值的 sqrt(vol) 缩放 |
| Schwartz-Bruhat | p-adic 局部常检验函数 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| modelXi + volP | 换格 sqrt(vol) 缩放 |
| movesCompose | 换格链复合律 |
| wPhase | (−1)^m 相位 |
| wCocycle（c² = kap）| 2-上循环 |
| PhiHat | p-adic 局部常函数 |
