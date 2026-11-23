# 数学背景 32 — Petersson 公式：均方界的引擎室

> 面向零基础读者。读完你将理解自守形式的 L² 内积公式——特征和均方估计的标准文献工具。

## 1. Petersson 内积：自守形式的几何

两个尖形式 f, g 的 Petersson 内积：

⟨f, g⟩ = 对模群基本域积分 f(z)·conj(g(z))·y^k · (dx dy / y²)

它把"函数"变成"几何"（内积空间），谱理论随之适用。

## 2. Petersson 公式：内积的谱展开

**Petersson 迹公式**（1930s）：⟨f, g⟩ 的展开式中，一边是 Hecke 特征值，另一边是 Class poly/Class 数对象——**特征值的谱求和与类数对象对账**。

对特征和均方的意义：

Σ_chi |L(1/2 + it, chi)|² 的均方 = 对偶形式的 Petersson 型积分

**均方估计（解读 18 的 MeanSquareBounds）的文献级工具就是 Petersson 公式**——"平均而言特征和是 sqrt 级"的严格来源。本引擎 LocalQuadraticParts 的 PeterssonBound 三件套（AtEmbedding/AllEmbeddings/FixedEmbedding）即其形式化。

## 3. 与引擎其他层的连接

- 均方界 ⇒ pairEx 好素数对存在（解读 18 大筛排除法）
- 均方界 ⇒ 窗口内 Gm 截断（解读 14）
- Petersson 展开 ⟷ Kato/Euler 系统（解读 15）的互补：一个从谱侧、一个从算术侧压 Sha/Selmer

## 4. 源码组织学注记

LocalQuadraticParts 的"局部二次部分"= L² 展开的二次项；三件 Petersson 界（按嵌入分类：All/Fixed/At）对应"嵌入不均匀性"的处理——CM 场景（Kstar）的嵌入对 (τ, conj τ) 需要区分对待。

## 术语速查

| 术语 | 一句话 |
|---|---|
| Petersson 内积 | 自守形式的 L² 几何 |
| Petersson 公式 | 内积的谱展开（特征值 ↔ 类数对象）|
| 均方估计 | 特征和平方的平均 |
| 周围形式（AmbForm）| 尚未定型的候选形式 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| PeterssonBoundAtEmbedding | 单嵌入版界 |
| PeterssonBoundAllEmbeddings | 全嵌入版 |
| AmbForm | 周围形式 |
| RRMetricDef / DivisibilityLatticeMetricCondition | 格度量条件 |
