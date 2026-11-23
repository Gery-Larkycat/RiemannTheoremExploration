# 解读 45 — NData 数据总线：引擎读数体系的统一规范

> 对应第四十五轮侦察。LevelLetterCocycles/DataN.lean（1186 行）——引擎读数体系的「数据总线」。

## 1. NData 结构体：全部读数数据的打包（55 行起）

NData (R : Ranks) (H : Host R) (what₂ : Rows.Data R) 打包：

- **Om**：H.E 的代数闭包（域 + 代数闭包实例）
- **plOm**：Galois 上同调位提升
- **ldat**：∀ 素数 p，**LData H.E Om p**（解读 04 的 Galois 上同调数据！）
- **sha_eq**：**LData.shaLen = 行表 shaLen**（两种 Sha 长度表示的一致性——解读 04 的 Statement.lean 与解读 26 的行表在此桥接！）
- **Loc/l/j/mu/w**：局部位置类型 + 素数标记（皆素数）+ 行范围（1 ≤ j ≤ m）+ 元组扭转绑定

⇒ **NData = 「每个素数 p 的上同调场景 + 局部行位置」的数据总线**——解读 04（LData）与解读 26（行表）的统一数据层。

## 2. NData 派生性质群（187-232 行）

- **Bj_rank**：Bj 模秩 = C 维数（有限秩一致）
- **ShaFin / ShaFinOdd / ShaFinTwo**：Sha 有限 / 奇指标 / 2-长有限——解读 04 Sha 理论的 NData 级表达
- **EigSpan**：Hecke 特征向量张成全空间
- **MtUp/MtLow**：张量积子模块上下界（分式域张量）
- **etaLoc**：局部 eta 有理数；**vdel**：p-adic 赋值求和（Σ s0 + padicValNat）

## 3. heckeEig/heckeMult：Hecke 特征理论正式化（15-27 行）

- **heckeEig T act x** := 所有 Hecke 算子 f 的特征空间之交（f(x) 为特征值）——**测试点 x 的 Hecke 特征子空间**
- **heckeMult** := 特征子空间的分式域维数——**Hecke 重数**

⇒ 经典 automorphic 谱理论（重数一定理语境）的正式化：**重数判分歧**（mult 大 = 特征退化）。

## 4. 驯化生成元与位分类（44-53 行）

- **TameGenAt**：γ ∈ 惯性群且惯性群 ⊆ closure(⟨γ ∪ tame⟩)——**γ 生成惯性群的驯化部分**（Wild/Tame 惯性理论——分歧群的驯化商由 γ 生成）
- **IsConjPl**：w 与 w' 互为共轭位（conj 对称）
- **IsSplitPl**：存在 x ∈ v.asIdeal 且 conj(x) ∉ v.asIdeal——**分裂位判据**（x 的共轭出位 = 分裂）

⇒ Wild/Tame 惯性 + 共轭/分裂位——局部 Galois 理论的完整体现。

## 5. 本轮结论

NData 是引擎「读数体系」的**统一数据总线**：上游（Galois 上同调 LData）与下游（行表/字母编码）在此对接（sha_eq 一致性）；Hecke 特征/重数/驯化生成元/位分类全部纳入同一结构。**引擎的数据架构 = NData 总线 + 各区消费**。

## 下一步侦察队列（按需）

- heckeEig/heckeMult 的消费链（谁用重数）
- NData 构造（哪里给出 NData 实例——数据总线从哪来）
- GL3Theta 前段 60-107 行补遗
