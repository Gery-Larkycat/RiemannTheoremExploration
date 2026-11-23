# 数学背景 46 — Speh 表示与酉对偶谱：GL(n) 的离散谱分类

> 面向零基础读者。读完你将理解「Speh 表示」这个 GL(n) 离散谱的标准对象，以及「酉对偶」为什么是算术的天然舞台。

## 1. GL(n) 离散谱与 Speh 表示

GL(n) 的自守表示谱分连续谱（Eisenstein，连续参数）与离散谱（尖形式 + 某类残差表示）。**Speh 表示**（Speh 1977-1983 构造）是 GL(n) 离散谱中非尖形式的代表——由「尖形式的张量积的残差」构造。

本引擎 RecSpehQuot/RecSpehPRecT：**递归 Speh**（递归构造的 Speh 商/配对）——GL(n) 谱的递归分解结构。

## 2. 酉对偶谱（Unitary Dual）

酉表示 = 保持 Hermite 内积的表示（物理：量子力学的对称性）。**酉对偶谱** = GL(n) 的全部酉不可约表示的分类（Langlands 分类 1979：酉表示由「 tempered 部分 × 正实压缩」参数化）。

引擎 UnitaryDualGL/exists_parts：**酉对偶的部分存在性**——从假设构造酉表示的组成部分（Langlands 分类的引擎化）。

## 3. Satake 参数与酉球形修正

球形表示由 Satake 参数（解读 15）完全决定。**UnitarySphericalFixing**：用酉条件「修正/固定」Satake 参数——参数必须满足酉性约束（|参数| 相关的对称性）。

PotentialCrystallinity（势晶体性）：参数在何时来自晶体表示（解读 31 斜率=Hodge 斜率）——**势晶体性 = 「可能是晶体的」判据族**。

## 4. 为什么要酉性

酉性保证表示的 L² 理论良好（Parseval/Plancherel 成立）——**均方估计（解读 18）的合法性前提**。非酉表示的 L² 理论需要特殊处理。引擎的谱分析全部在酉范畴内进行（酉性是 HostGood/窗口的隐含前提）。

## 术语速查

| 术语 | 一句话 |
|---|---|
| Speh 表示 | GL(n) 离散谱非尖代表 |
| 酉对偶谱 | 酉不可约表示分类 |
| Langlands 分类 | 酉表示的参数化定理 |
| Satake 参数 | 球形表示的完全不变量 |
| 势晶体性 | 「可能来自几何」判据 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| RecSpehQuot / RecSpehPRecT | 递归 Speh 商与配对 |
| UnitaryDualOfHyp / exists_parts | 酉对偶部分存在 |
| UnitarySphericalFixing | Satake 参数酉修正 |
| PotentialCrystallinity | 势晶体判据族 |
| InertialTypeOfTameM | 驯化惯性型 |
