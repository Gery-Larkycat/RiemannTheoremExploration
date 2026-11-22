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

## 引擎侧发现（第二轮侦察补充）

- GlobalTheory.Published 文献库：LocalLanglandsGL(1228) / CuspRapidDecay(1133) / HarishChandraModules(600) / GlobalArtinReciprocity(527) / CasselmanWallach(421) / HoweDualityReal(208) 等——文献定理一次性接入
- WeilBound = Theta/Siegel-Weil/Eisenstein 分析机器（RegularisedSiegelWeil、SiegelEisensteinHalfPlane/SchwartzBruhatMajorants、ThetaLifts、FiniteTypeHarishChandra/GreenCuspidal）
- 组装点 TopPlug.lean（19 行）：Green + VWin + HypsAlt ⇒ ZeroFreeAll；常数 la := 3/2 反复出现
- EveryCharacterE.lean 配料：BhattScholzeCrystallineLattices / PrismaticDieudonne / SatakeParameters / WeilConvergenceOfSiegelSet / GlobalInterpolation
- 新概念嫌疑升级：LiteralAutomorphy（字面自守性/rowRatW 行有理性）、BoundAtTwoAndThreeForFamily（2、3 处的界）、CovTop.CovolX、IndefiniteRowSideFullHecke.WeilTensorModels
- 解读系列：docs/walkthrough/01-主线收束链.md、02-引擎深潜.md

## 窗口不等式解剖（第三轮侦察补充）

- VWin 四层结构：VWin(401) → VWinAt(eps<1/52, PageN, WinPair, [Y,Y²]) → VAt(IsChiField ⇒ VVle) → VVle(Sha 长度指数和 ≤ e^(x^eps/2))
- WinPair：q≡3 mod 8、d≡7 mod 16、q|d+1、d+1 小素因子只有 2 和 q——手工调音的素数对
- IsChiField：ψ + 2^(e+2) + q + d 的 Jacobi 特征联合切出的分圆子域（Galois 固定域判据）
- VVle：Galois 上同调数据 LData 的 shaLen 行表加权指数和 ≤ B——**Brauer 类群塔方法的升级版**
- Green 定理 = 有限域 GL_d(F_p) 的标签-表示字典（LabelDatum/LabelConv/HasCuspLabel，namespace PositivityTheory.GreenCharacters）；非分析 Green 函数
- LData 定义于 Formalism/GaloisCohomology/Statement.lean:54；shaLen : ℕ → ℕ → ℚ
- Formalism.HC 驻扎 PrimeDiscriminants（RamDiscr/CycImage/HostRaw）——Host（宿主）概念家族待解剖
- 解读系列新增：docs/walkthrough/03-窗口不等式与Green字典.md；数学背景笔记 03

## Poitou-Tate 引擎核心（第四轮侦察补充）

- LData（GaloisCohomology/Statement.lean:54）= (F 的 l-位集 S、位提升 A、分圆 l-adic 特征 chi)；QZ l = Q_l/Z_l
- qzTw/zlTw = Tate 扭转；Sha/shaLen = 分圆扭转的 H¹ 限制核及其长度；VLen = H²(Z_l(e+1)) 长度
- 四条 PT 假设（PTCokerAt/PTShaAt/TateLocalDuality/有限长度）⇒ **VFormula**：VLen + H⁰ = shaLen + Σ局部H⁰ —— VWin 之 V 同源于此
- Selmer 框架：unrAt/bkCond/SelAll/selLen；InfUnram 无限位不分歧判据；Indep 长度不变性；LDataExists 存在性
- 引擎故事线：素数对 → IsChiField 域 → LData → PT 长度平衡 → Selmer 长度解析估计 → 显式公式 → L 非零
- 缺口：解析侧如何估计 Selmer/Sha 长度（shapeWin/supplyChi 定位于 CharacterBoxes/，下轮解剖）
- 解读系列新增：docs/walkthrough/04-PoitouTate引擎.md；数学背景笔记 04

## Host 舞台与组装总装（第五轮侦察补充）

- 类型系统：HostReq/FReq 均为 Type 1 要求函数（命题级依赖注入）
- HostGood 十四条：范数方程 π·conj(π)=g_i（(π−1)∈⟨QS·q·d⟩）、pde/pde' ≡ 1 mod lcm(15, QS·q·d)、q0 ≡ 1、levelPrimes 五素数、BoxW 窄窗、|dlogH| ≤ x^eps、ThinOK/BadOK
- GChi ψ := EAtH(Level.cyc ψ) ∧ VVle H.E——特征要求 = 循环实现 + 宿主 Sha 窗口
- **BoxW.real_ne_zero：宿主上的 L 在 β > 1−1/400 无零点（400 常数；401 = VWin 截断，常数网成形：401/400/52/3/2/15）**
- 组装总装：shapeWin(Green→TopShape/TopG) + supplyChi(VWin→HostExW 3/2) → zeroFreeAll_of_topG(la>1) → ZeroFreeAll
- 新线索：zeroFreeOn_of_tiedWin_cyc（薄化放大定理本体）、ChainTied、Scales la 尺度几何、GlobalInterpolation Link* 链接网络
- 解读系列新增：docs/walkthrough/05-Host舞台.md；数学背景笔记 05

## 下一步侦察队列

- [ ] GlobalTheory.GLq.Green 的定义与数学含义（引擎全局输入）
- [ ] UpperTheory.Top 全家：VWin / shapeWin / supplyChi / imprimitive
- [ ] Hyps / LinkN / DRS 假设系统的语义
- [ ] Formalism.HC.ZeroFreeAll 的内容（HC 是什么）
- [ ] Formalism 顶层 40+ 目录逐个定性，区分"标准数学形式化" vs "新工具"
