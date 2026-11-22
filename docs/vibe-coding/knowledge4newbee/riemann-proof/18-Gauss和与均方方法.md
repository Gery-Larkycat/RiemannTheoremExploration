# 数学背景 18 — Gauss 和与均方方法：特征和的傅里叶视角

> 面向零基础读者。读完你将理解"Gauss 和"是什么、均方估计为什么强大，以及"好素数对存在"的排除法逻辑。

## 1. Gauss 和：特征和的傅里叶变换

对模 q 特征 chi，Gauss 和定义：

tau(chi) = 对 n mod q 求和 chi(n) · exp(2·pi·i·n/q)

它是 chi 与加法特征（指数函数）的"内积"——**乘法世界与加法世界的接头暗号**。基本性质：

- 非主特征：|tau(chi)| = sqrt(q)（恰好平方根！）
- 它是函数方程的构建材料（解读 01 镜子的零件）
- 它把"乘法相消"翻译成"加法相位"——傅里叶变换的经典把戏

## 2. 均方方法：平均意义上的小

逐点控制特征和 S(x) = Σ chi(n) 很难（解读 11 的 Schur 天花板）。**均方方法**换个问题：

(1/X) 对 chi 求和 |S(chi, x)|² 的平均有多大？

均方小 ⇒ 大多数特征的大多数点都小 ⇒（用大筛/排除法）**坏点稀少** ⇒ 对任意给定的特征，好窗口存在。

**pairEx（素数对存在定理）正是这个逻辑**：在均方估计下，"坏素数对"（BadShare/CountBad）稀少，排除掉它们，剩下的就是"好对"（PairExists）——supplyOfAdmOf 拿到的 QH.pairEx 即此。

## 3. 大筛思想的精确化

大筛法（Linnik 1941，Gallagher 简化）：若一族对象（素数对）在每个"模"处都稀疏，则整族稀疏。引擎的 MeanSquareBounds 区：

- 均方估计（meanSqK/MeanSqAbs）——"平均小"
- CountBad/BadShare——"坏份计数"
- kappa4loglog/kappaC——loglog 尺度的常数精细度
- Stage1Succ/StagePow——多阶段推进（大筛的迭代版）
- SmallZeros——"小零点"集合的处理（与零点自由的接口）

## 4. Shintani 公式与逆定理（背景预览）

- **Shintani 公式**：GL(3) 的显式迹公式类对象（对角情形）——谱侧求和的显式化
- **逆定理（Converse Theorem）**：Cogdell–Piatetski-Shapiro：若一个 GL(n) 型 Euler 积分/级数有足够好的解析性质（延拓、有界），则它**来自自守表示**——"好性质 ⇒ 自守"的反向判定

引擎用它保证：从宿主舞台读出的 L 函数波，其好的解析行为**合法地**等于自守对象的贡献——波的"户籍"被登记。

## 术语速查

| 术语 | 一句话 |
|---|---|
| Gauss 和 | 乘法特征与加法相位的内积，模长 sqrt(q) |
| 均方估计 | 特征和平方的平均 |
| 大筛法 | 逐模稀疏 ⇒ 整族稀疏 |
| pairEx | 好素数对存在定理 |
| Shintani 公式 | GL3 谱求和显式化 |
| 逆定理 | 好解析性质 ⇒ 自守性 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| GaussSumFunctionEq.lean | Gauss 和恒等式 |
| meanSqK / MeanSqAbs | 均方量 |
| pairEx.lean | 好素数对存在定理 |
| CountBad / BadShare | 坏份计数与分摊 |
| ConverseTheoremConstantTerm.lean | GL3 逆定理常数项 |
