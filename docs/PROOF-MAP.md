# 证明地形图（阅读进行时）

> 自顶向下追证明主干的过程记录。阅读约定：只读定理**声明**（数学内容），跳过证明体（tactics 由内核负责验证）。

## 主线收束链（已闭合，全部人类可读）

- Main.lean (12行)
  - Supplements/Kernels/MainTheorems.lean (16行)
    - allChi : UpperTheory.EveryCharacter = UpperTheory.FinalTheorems.everyCharacter（引擎顶点，声明在 CharacterBoxes/EveryCharacter.lean:13）
    - rhOfAll : RiemannHypothesis = Formalism.VW.rh_of_every allChi（Formalism/GammaFactorNonvanishing/CritLine.lean:29，32 行桥文件）
    - critAll / claimAll：GRH 临界带版本（同走 critLine）

### 主线的数学结构 = Hadamard–de la Vallée Poussin 经典复活

Formalism.VW.critLine（CritLine.lean:11）证明链：

1. **Γ 因子非零**（gammaFactor_ne_zero）：偶/奇特征分别用 GammaR 的正实部非零性
2. **右侧非零即一切**：EveryCharacter 只保证 Re(s) > 1/2 处 L(s,χ) ≠ 0
3. **函数方程反射**：χ⁻¹ 也是本原特征；完成 L 函数满足 χ ↔ χ⁻¹、s ↔ 1−s 对称；Γ 因子非零 ⇒ 左半带零点反射为右半带 L 零点，与 EveryCharacter 矛盾
4. **ζ 情形**：rh_of_every 用模 1 主特征退化（LFunction_modOne_eq），经 RhOfRight 收口

⇒ **证明的全部新数学在引擎侧**：UpperTheory.EveryCharacter（∀ 特征 ∀ s, Re(s) > 1/2 ⇒ L ≠ 0）。

### 引擎顶点的组装配方（EveryCharacter.lean）

- plugWin : GlobalTheory.GLq.Green（全局理论：GL_q 的 Green 函数，谱几何对象）
  - + UpperTheory.Top.VWin（V-窗口不等式，每个特征一个）
  - + Hyps(... LinkN Fm ... DRS)（假设系统：闭包/链接/DRS 谱）
  - ⇒ Formalism.HC.ZeroFreeAll（HC 零点全消）
- plugAll : plugWin + imprimitive（非本原特征补齐）⇒ EveryCharacter

## 规模分布（行数占比）

| 库 | 行数 | 占比 | 角色 |
|---|---|---|---|
| Development | 12,232,663 | 70.4% | 朗兰兹机器全套（阿贝尔簇/Theta/迹公式/Galois 表示/étale）|
| Formalism | 3,200,748 | 18.4% | **形式桥网络 + 新工具家族** |
| GroundTheory(+Fields) | 1,119,138 | 6.4% | 基础理论 |
| ReciprocityTheory | 563,016 | 3.2% | 互反律（约化群环面紧化等）|
| CompanionTheory | 194,218 | 1.1% | 谱几何/Harish-Chandra/Eightfold |
| PositivityTheory | 55,130 | 0.3% | 正性理论 |
| Lemmata | 9,232 | 0.05% | 引理（出乎意料地小）|
| Supplements+BuildAid | 42 | ~0 | 收束点 |

总声明数 971,932；import 枢纽 top3 全在 Development.AbelianVarietyTheory.Definitions.Divisors。

## 新数学结构候选清单（持续追加）

1. **UpperTheory（上界理论）**——统一"每个特征一个窗口不等式"的上界体系（VWin / shapeWin / supplyChi）
2. **GlobalTheory.GLq.Green**——GL_q 层次的 Green 函数；证明引擎的全局输入
3. **Formalism 形式桥网络**——RH 与各种可攻命题的等价翻译层（PowerBoundGivesRiemannHypothesis、HalfLinks、SizeWindowBrackets、ChainCore 等）
4. **CharacterBoxes（特征箱）**——Claim.Strip / Claim.Zeta / HalfPlane 的方法家族，含 PairGood/PairRows 配对法
5. **GammaFactorNonvanishing**——Γ 因子非零性形式化（桥的地基）
6. **EightfoldProjection**（CompanionTheory 侧，Zarhin 技巧内）——待查
7. **SharpRestriction / LocalRingCardinality / FockGram / GelfandTransference**（Formalism 内）——名字即嫌疑工具，待查

## 下一步侦察队列

- [ ] GlobalTheory.GLq.Green 的定义与数学含义（引擎全局输入）
- [ ] UpperTheory.Top 全家：VWin / shapeWin / supplyChi / imprimitive
- [ ] Hyps / LinkN / DRS 假设系统的语义
- [ ] Formalism.HC.ZeroFreeAll 的内容（HC 是什么）
- [ ] Formalism 顶层 40+ 目录逐个定性，区分"标准数学形式化" vs "新工具"
