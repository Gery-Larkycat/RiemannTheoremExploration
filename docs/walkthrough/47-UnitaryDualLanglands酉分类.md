# 解读 47 — UnitaryDualOfHyp：Langlands 酉分类的递归构造

> 对应第四十七轮侦察。UnitaryDualOfHyp.lean 双定理全解——酉对偶谱分类的引擎化。

## 1. exists_part'：部分存在（a·d = n 乘积公式）

输入：离散谱（DiscreteSpectrum）+ 尖温度（TempCsd）+ 递归 Speh 理论（RecSpehT）+ 尖读取（CuspRead）+ n 维离散尖子空间 V（IsCsdGL）+ **无穷特征多重集 m(τ) 无重复且全部 = g + 整数**（权重平移结构）。

输出：存在 **Part p：1 ≤ p.a ∧ 1 ≤ p.d ∧ a·d = n**，A.csd p.π（尖离散），且：

- 局部紧条件 ⇒ **IsUnitarisable σ.ρ**（可酉化）∧ **rc w n σ = spehLoc**（递归映射 = 局部 Speh）
- 无穷特征 ⇒ m = **spehInf p.d**（Speh 无穷谱）

**a·d = n 正是 Speh 构造的乘积公式**：Speh 表示 = 尖形式（维 d）× 分段参数（维 a），乘积给 GL(a·d) 的离散谱——Langlands–Speh 离散谱分类的引擎化！

**特征值结构 z = g + k**：全部无穷特征是同一 g 的整数平移——**Hodge-Tate 权的平移结构**（解读 16 Deligne 表示的权）。

## 2. exists_parts'：多重部分存在（Langlands 酉分类递归构造）

更强输入加文献两件：**Published.BaseChangeDefiniteUnitary**（基变换定酉——文献级）+ **BernsteinUnitaryProductIrreducible**（Bernstein 酉积不可约）+ 递归结构全套（RecProd/RecSpehT/RecSatake/RecMap）。

输出 **Pa : List Part**：全部合格 ∧ **rankIso N A Pa = n**（部分秩和 = n）∧ 三条精细性质：

- 分裂位 w：存在局部不可约 σ，IsCompAlong ∧ **isoLoc N A Pa w = rc w n σ**（局部同构匹配递归映射）
- 未分歧 alpha：**A.unr ∧ frobEig = ubc(单位群像)**——**未分歧 Frobenius 特征值落在单位群映射像中**
- HasWeightAt：**Pa.Nodup ∧ isoInf = infOfWeight ∧ 共轭位 = 负权重**——**Hodge-Tate 权结构**（共轭嵌入带负权）

证明骨架：hNT（BaseChange 文献）分解 n 维 → hnd 无重复（从权重）→ hg 权平移结构 → choose p（逐部分调 exists_part'）→ Q 组装（locProd 乘积 + isSmooth + isIrreducible 经 BernsteinUnitaryProductIrreducible）。

## 3. 语义综合：酉对偶谱分类的引擎化

UnitaryDualOfHyp = **Langlands 酉分类定理**（1979）的引擎形式：n 维离散尖谱 → Speh 部分列表（a·d = n）→ 分裂/未分歧/无穷三位的完整不变量（局部同构/Frobenius 单位群/权重平移）。

结合解读 16 KatoLitO（Deligne 表示 + Selmer 有限）——**「Kato 供有限、UnitaryDual 供分类」的双支柱谱理论**完整。

## 下一步侦察队列（按需）

- RecMap/RecProd/RecSatake 递归结构定义
- NAut 定义（自守酉化）
- GL3Theta 前段 60-107 行补遗
