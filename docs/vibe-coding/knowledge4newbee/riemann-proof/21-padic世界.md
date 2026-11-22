# 数学背景 21 — p-adic 世界：另一种绝对值下的微积分

> 面向零基础读者。读完你将理解 p-adic 数的基本直觉，以及为什么它成为数论的"第二语言"。

## 1. 两种绝对值

同一有理数 1/2，两种度量：

- 通常绝对值：|1/2| = 1/2（小于 1）
- p-adic 绝对值（p=2）：|1/2|_2 = 2（大于 1！）

p-adic 绝对值按"p 整除程度"打分：n 整除 p 越多次，|n|_p 越小。**在 p-adic 眼里，大的幂 p^k 是"接近零"的小数**。

## 2. Q_p 与 Z_p：完备化的新世界

按 p-adic 绝对值补全有理数得到 **Q_p**；其中的"p-adic 整数"（|x|_p ≤ 1）构成 **Z_p**。本引擎的记号：

- Q_p 记作 Q_[p]，Z_p 记作 Z_[p]（源码 QZ l = Q_l / Z_l 的底座）
- **C_p**：Q_p 的代数闭包完备化（复数 C 的 p-adic 类比）——GL3Theta 的幂级数系数就住在 C_p

## 3. p-adic 微积分：收敛换了一套规则

- 幂级数 Σ a_n x^n 在 C_p 上收敛的条件是 |a_n x^n|_p → 0——与复分析完全不同的区域几何
- **积分性**（IntegralW/CoefWf：系数都是 Z_p 整点）是 p-adic 级数"良好"的标准
- logMv：多元幂级数的 log——p-adic log 有自己的收敛域

GL3Theta 用这套语言描述 GL3 Theta 对应的 p-adic 侧：tauK（Gauss 和的 p-adic 化身）从宿主域元素 a 与嵌入 lam 出发构造——**同一个算术对象在复世界与 p-adic 世界的两张面孔**。

## 4. 为什么数论需要两套世界

- 复分析管"竖直线上的大小"（解析延拓、函数方程、零点位置）
- p-adic 分析管"同余与分歧"（局部类域论、Euler 系统、Iwasawa 理论）
- **算术对象的完整肖像需要两张照片**：本引擎的 Poitou-Tate（上同调，本质 p-adic）与 Landau/Mellin（解析，本质复）正是两套照片的对照阅读

## 术语速查

| 术语 | 一句话 |
|---|---|
| p-adic 绝对值 | 按 p 整除深度打分 |
| Q_p / Z_p | p-adic 补全 / p-adic 整数 |
| C_p | Q_p 的代数闭包完备化 |
| 积分性 | 系数落回 Z_p 的良好性 |
| tauK | Gauss 和的 p-adic 化身 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| Wp / InWf | Z_p 子环与积分点 |
| MvPowerSeries sigma Cp | C_p 上多元幂级数 |
| logMv / SimeqW | 多元 log 与加权相似 |
| tauK / tauKc | p-adic Gauss 和 |
