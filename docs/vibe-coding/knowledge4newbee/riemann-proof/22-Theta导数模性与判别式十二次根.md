# 数学背景 22 — Theta 导数的模性与判别式十二次根

> 面向零基础读者。读完你将理解"Theta 级数的导数在特殊点的值为什么算得出来"，以及判别式的 1/12 次幂为什么无处不在。

## 1. 判别式的 1/12：解析类数公式的签名

虚二次域 K = Q(√−d) 的解析类数公式：

h(K) · 常数 = (√|disc| / 2π) · L(1, chi_d) 相关量

其中判别式以 **|disc|^(1/2)** 幂出现。zeta 的残差公式同样带 discr^(1/2)。**判别式十二次根**（本项目 IsDiscriminantTwelfthRootOfIdealLattice）是这些公式在"理想格"对象上的代数化身：格的行列式（体积）与判别式的幂对应——12 = lcm(2,3,4) 来自各处公式的最小公倍需求。

一句话：**判别式的幂 = 域的"体积"在所有公式中的统一计量单位**。

## 2. Theta 导数的模性（Kudla 理论直觉）

Theta 级数对"检验函数"求导后，导数级数的系数是**几何量的计数**（比如某格点集合的高度和）。Kudla 的洞察：

**Theta 导数在自守点的值 = 某些特殊零维/一维循环的高度和，且这些和是模形式/自守形式**

—— 即"Theta 导数的模性"（Kudla-Rapoport-Zhang 等发展成大理论）。本引擎的 TwistedThetaTheorem → RelativeDeterminantEquation + 矩条件群正是：**扭曲 Theta 的模性结论被写成"相对判别式方程 + 各阶矩的界"**。

## 3. 为什么这能喂饱"高度与消失"

解读 18 的 HeightAndVanishing 区（BchiFacts/Count 族/GdOfHost）：

- **高度**：类群元素的（对数）高度由判别式根控制（TaylorLogMetric）
- **消失**：Theta 导数的某些矩为零/很小（mom22/str22 条件）⇒ 类群上的求和大量消失 ⇒ 存活项可枚举（Count 族）⇒ Gd/Green 读数有界

**"高度高 ⇒ 消失多 ⇒ 界小"**——这是宿主窗口读数（a(t), b(t) ∈ 窄窗）的数值来源。

## 4. Frobenius 读数：抽象与具体的对表

Reads D psi chi：chi(p) = psi(Frob_p)（未分歧 p）。这是 Artin 互反律的接口形式：

- 抽象侧 psi：宿主类域 Galois 群的特征（几何/表示对象）
- 具体侧 chi：Dirichlet 特征（可进 Landau/Mellin 机器）
- **互反律保证两侧信息等价**；引擎用 Reads 把抽象量全部翻译到具体侧计算，再用互反律把结论传回抽象侧

## 术语速查

| 术语 | 一句话 |
|---|---|
| 解析类数公式 | h·R 与 L(1) 的恒等式，判别式平方根入场 |
| 判别式十二次根 | 理想格体积的统一计量 |
| Theta 导数模性 | 导数级数 = 循环高度和（Kudla）|
| 未分歧素数 | p 不整除判别式 |
| Frobenius 读数 | chi(p) = psi(Frob_p) 的对表 |
| 相对判别式方程 | 格相对体积的精确关系 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| Reads / prim | Frobenius 读数对接 |
| Unram / InertK | 分歧/惯性分类 |
| TaylorLogMetric | 对数量规（高度）|
| IsDiscriminantTwelfthRootOfIdealLattice | 判别式十二次根格 |
| mom22 / th22 / int22 / str22 | 矩/积分/结构条件群 |
| KudlaFamilyStatement | Theta 导数模性族化 |
