# 数学背景 47 — Langlands 酉分类与 Speh 乘积公式

> 面向零基础读者。读完你将理解 GL(n) 离散谱的分类定理（Langlands 1979），以及 Speh 构造的乘积公式 a·d = n。

## 1. 问题：GL(n) 的离散谱由什么组成

GL(n) 的自守离散谱 = L² 中不可约子空间的组成成分。**Langlands 分类**（对一般实群）与 **Moeglin-Waldspurger**（对 p-adic GL(n)）给出答案：

离散谱表示 = **Speh 表示**，由「尖形式 π（维 d）× 分段参数 Δ（维 a）」构造，维数 = a·d。

**乘积公式 a·d = n**：GL(n) 的离散谱部分必须分解为 a×d 的乘积——这是「谱的因式分解定律」。

## 2. Speh 构造直觉

取尖形式 π（GL(d) 的）与分段参数 Δ（长度 a），构造残差表示：

Ind(π|·|^{Δ₁} ⊗ π|·|^{Δ₂} ⊗ … ⊗ π|·|^{Δ_a}) 的某个残差

参数 Δ 是长度 a 的递减序列（区间 [x, x+a−1] 的离散化）——**Speh 表示的参数是一个区间**！这是 p-adic 谱理论最美的定理之一。

## 3. 酉性与权重

酉表示的 Hodge-Tate 权有对称性：**权重集合关于中心对称（共轭位带负权）**——本引擎 isoInf(共轭 τ) = −infOfWeight 正是此对称。

## 4. 引擎化意义

UnitaryDualOfHyp 把这个分类定理变成**递归构造程序**：n 维谱 → Speh 部分列表 → 每部分继续递归。递归的每层使用文献定理（BaseChange/Bernstein）——**「分类定理 = 递归程序」的架构**。

## 术语速查

| 术语 | 一句话 |
|---|---|
| Speh 表示 | GL(n) 离散谱非尖代表，参数为区间 |
| 乘积公式 a·d = n | Speh 维数 = 尖维 × 分段维 |
| 酉对偶谱 | 酉不可约表示分类 |
| Hodge-Tate 权 | p-adic Hodge 结构的权重 |
| 基变换 | 群扩张下的表示迁移 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| Part 的 a·d = n | Speh 乘积公式 |
| rankIso Pa = n | 部分秩和 = n |
| spehLoc / spehInf | 局部/无穷 Speh 谱 |
| BaseChangeDefiniteUnitary | 基变换定酉（文献）|
| BernsteinUnitaryProductIrreducible | Bernstein 酉积不可约（文献）|
