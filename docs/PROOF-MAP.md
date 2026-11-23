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

## 放大机制贯通（第六轮侦察补充）

- Scales la：J + Win 窗口集 + windows（对每个 y 存在 Y 使 [Y, Y^la] 全在 Win 内）——**la = 覆盖指数，3/2 的结构角色**（VWinAt 的 [Y,Y^2] 是 la=2 特例）
- TopWin.lean 组件族：WinAll / ChebyshevInequalityOnWindows(Λ=Level.cyc psi) / TiedAll / ExWin / ChainWin → zeroFreeOn_of_tiedWin_cyc(la>1) ⇒ ZeroFreeOn
- ZeroFreeOn := 每个特征 psi.ZeroFreeAbove(1/2)；定义于 ExplicitFormulaErrorOfHostConditions.lean:11-14
- ChainTied（TieGlobal.lean:97）：读数 av/bv + Data/Word/Top 组合编码 + TiePts/TieGlobal/TieLocal/TieArith 四绑定 + **Ident（primVal 与 ell psi = logDerivativeAtOne chi 即对数导数）** + LChain.SizeData2/ErrWindows/BNBounds
- **引擎总图闭合：经典 de la Vallée Poussin 骨架（切比雪夫窗口上界 => 对数导数控制 => 右半带无零）× 新燃料（宿主舞台供给上界：Poitou-Tate Sha 窗口 + 标签字典 + 链接网络）**
- 解读系列新增：docs/walkthrough/06-放大机制.md；数学背景笔记 06

## 平方根截断与 Landau 判据（第七轮侦察补充）

- **核心不等式**：ChebyshevInequalityOnWindows（TopDefs.lean:26）结论 = Λ.Gm x ≤ x^(1/2 + (eD+eL+7)·eps)——平方根截断，GRH 等价语言
- Landau.lean（592 行）：logDerivZeroFree 判据（P'=qP 正实部 ⇒ 无零点）+ re_gChi（复值量实部 = Gchi 正项和）+ sumLamChi（von Mangoldt 求和）——**Landau 1918 技巧引擎版**
- Level 层 = InertJacobiLevels（48 文件）：两素数域（TwoPrimeFieldMemLevelOfCoprime）+ Jacobi 惯性类 + TiesAtY/Core/Asm/Lat 绑定族 + HostFam + VVEqEmpty
- ExWin + ChainWin ⇒ AtWindowScale（tiedWin_of_ex 组合引理）
- 引擎范式：正项和截断 ⇒ 指数型实部控制 ⇒（Landau 判据）零点自由
- 剩余缺口：Gm 精确定义、LChain 代数定义、supplyOfAdm 构造、ExplicitFormulaError 本体、常数 7 出处
- 解读系列新增：docs/walkthrough/07-平方根截断与Landau判据.md；数学背景笔记 07

## Gm 与窗口化零点判据（第八轮侦察补充）

- **Gm 定义**（ExplicitFormulaErrorOfHostConditions.lean:38）：Gm y = Gz y + Σ_{ψ∈Λ.Nt} wt ψ · Re(gChi ψχ y)——显式公式的引擎版（主项 + 加权特征正项和）
- **零点判据桥**（:41 与 Window.lean:31）：Gm ≤ y^θ 的集合被 [Y,Y^la] 覆盖 ⇒ ZeroFreeAbove θ；反证形式（:26）若 Re>θ 有零点则窗口内 y^θ < Gm y
- **供给端装配线**（ShortNorms/supplyOfAdmOf.lean）：PairGood + VWinAt ψ 401 + admissible ⇒ 实例化 Host（HostGood）+ EAtH + VVle ⇒ HostExW(3/2)；装配细节 fieldChi → winPairs → C0/K/A 常数链（A = K^(5/eps)）
- 新词汇：Shares（分摊 x^(-1+eps)）、admitted、FieldRows、EventuallyRankLeRpow（1/52 出处）
- 逻辑链终局闭合（PROOF-MAP 第 4 节）：PairGood+VWinAt → 宿主实例化 → HostExW → TopG → Chebyshev 窗口 → 判据桥 θ→1/2 → RH
- 剩余缺口：Gz 定义、LChain、Link 网络、常数 7、ExplicitFormulaError 本体
- 解读系列新增：docs/walkthrough/08-显式公式函数Gm与窗口判据.md；数学背景笔记 08

## Gz 主项与引擎语义完全体（第九轮侦察补充）

- **Gz 闭式**（GzEq.lean）：Gz y = An.G y = Deduction.G y = Σ_{n≤⌊y⌋} vonMangoldt(n)·(y/n − 1)——主特征正项主项（log(y/n) 的线性下近似）；三表示统一（Formalism/An/Deduction.ramp）
- **FamilyClassConnected**（DivinNOfHypV.lean:13）：每 eps 层级存在窗口族 Fm，族内所有大窗口点 ChainTied 覆盖——族连通 = 绑定覆盖
- **HypV**（同文件）= 族内每宿主 VVle Sha 窗口成立——plugWin 之 V 的族化
- **vvRecord**：VVle ⇒ ShaFinOdd（genus 奇指标）+ vvTerm 级数收敛 ≤ B（vvTerm = log l·Σ shaLen）
- Gm = 主项(Gz) + 波(加权 gChi 实部和)——ζ/L 分离的引擎同构
- 剩余缺口（技术性）：LChain/LHost 物理路径、常数 7、Link 网络细节、ExplicitFormulaError 本体
- 解读系列新增：docs/walkthrough/09-Gz主项与族连通.md；数学背景笔记 09

## 条件主定理双璧与命名空间组织学（第十轮侦察补充）

- **PowerBoundGivesRiemannHypothesis.lean 全文**：双条件主定理——(1) LandauZeroFreeHalfPlane：Gz y ≤ y^theta => zeta 在 Re>theta 无零点；(2) PowerBoundGivesRiemannHypothesis：Gz x ≤ x^(1/2+C·eps)（每个 eps 最终恒成立）=> RH。**RH 当且仅当 Gz 增长指数 = 1/2**
- Gz = 主特征主项（解读 09）；zeta 通道（Gz 素数计数一己之力）与 GRH 通道（EveryCharacter 全特征压制）并行；实际证明走 GRH 通道（rhOfAll 经 rh_of_every）
- **命名空间组织学**：LFunctionChainParameters 家族物理实现在 SizeWindowBrackets/（64 文件 / 28,345 行；namespace 与路径解耦，LChain6/LHost/LBrDiv/LBr2 多轮生成痕迹；ChainSlopeWindows/ 子目录 = 常数预算推导地）
- 全库 157 文件引用该家族、0 个 import 行——逻辑架构与物理架构是两套坐标系
- 常数 7 澄清：exists_small_eps (eD+eL+7) —— 误差预算打包常数（非深奥常数）；另 (7:ZMod 16)^k 群论性质对应 d≡7 mod 16
- 解读系列新增：docs/walkthrough/10-条件主定理双璧.md；数学背景笔记 10

## RhOfRight 与 Schur 界目录（第十一轮侦察补充）

- **RhOfRight 全文**（Mathlib 级简洁）：hz（右半带无零）+ riemannZeta_one_sub 函数方程反射；cos 零点 ⟺ 负偶数（平凡零点排除）细节精确；与 critLine 同构的 Mathlib 原生版实例
- hz 供给 = EveryCharacter 模 1 主特征退化（LFunction_modOne_eq）——GRH 通道结论获源码印证（ζ 通道封口定理存在但数据源仍是 GRH 通道）
- **GlobalSchurBounds 定性初探**：GL3Columns/GL3Theta/AdmittedWeylDimension（GL(3) 侧机器）+ Joints 接合点群 + **LinkGLOBAL7Tied4 / ConclusionR7abs**（层级常数 7、4 进入文件名——7 的第二处身份嫌疑：链接层级）+ FlipTwoThree（2-3 翻转，呼应 q≡3/d≡7 mod 8/16）+ 编号化引理链
- SharpRestriction 子目录群 = "平方根截断构造图纸区"
- 解读系列新增：docs/walkthrough/11-RhOfRight反射封口.md；数学背景笔记 11

## 装配主车间与 GL4 分支链接（第十二轮侦察补充）

- **装配主车间**：RiemannHypothesisOfEveryCharacter.lean（231 行）= rhOfAll 供给链实体；imports 配料表含 SiegelWeil 酉收敛、Satake 参数、离散系列分类、Gauss-Manin 周期、**SiegelKlingenDeligneRibetOfBoth（特殊值定理群）**、Eisenstein 延拓、晶体 deRham——权威的"证明用了哪些数学"清单；第 213 行 modOne 退化入口
- **LandauTheorems 工具箱**（DedekindLFunctions/，36 文件）：Landau 九件套（Cauchy/Dichotomy/Finite/GrowthContra/KernelMax/Nearest/PoleAsym/PoleReLe/Coeff）+ CharFamilyLFunctionNeZeroOfOneLeRe（族版主项判据）+ MellinRamp——与 TotientGaloisClasses/Landau.lean 构成上下两级
- **GL4 分支链接**：LinkGLOBAL7Tied4 运行于 GL4（GlobalTheory/GL4/，BranchingLinkFamilyNormalised/ColumnLatticeExactSlope）；链接层级坐标初定（GLOBAL7 = 全局层级，Tied4 = 绑定层级）；GL3/GL4 并存 = Theta 提升梯子
- 架构六层图（层 0 收束 / 层 1 桥 / 层 2 引擎组装 / 层 3 解析机器 / 层 4 几何机器 / 层 5 文献）见解读 12
- 解读系列新增：docs/walkthrough/12-装配主车间与Landau工具箱.md；数学背景笔记 12

## 双装配通道与类数三临界件（第十三轮侦察补充）

- **装配车间尾部**（RiemannHypothesisOfEveryCharacter 211-231）：zeta_ne_zero_of_everyCharacter（一行主特征退化）+ riemannHypothesis_of_everyCharacter（完成函数对称版反射；Gamma 零点分类收尾）——与 CritLine 版同构不同封装
- **双通道确认**：通道 A = CritLine.rh_of_every（MainTheorems 主线）；通道 B = MainConclusion → RiemannHypothesisOfEveryCharacter（Main 闭包内）；RH 结论被 EveryCharacterOfLiteratureOfVWin / TemperedProductOfSquareIntegrable 等子系统复用为构件
- **MainTheoremsCritical = 类数三临界件**：SmallClassNumbers 三件（ClassNumberThree/LenEqZeroIff/OnePoint）——小类数边界情形修补层首例
- 解读系列新增：docs/walkthrough/13-双装配通道与类数三临界.md；数学背景笔记 13

## Landau 二分法与 Level-3 退化（第十四轮侦察补充）

- **LandauDichotomy 全文**（91 行）：landau_dichotomy 二分定理——左支真空半径 D（Z 与 B(σ,D) 不相交 + 最右点），右支孤立实点 β；landau_finite（局部孤立⇒紧内有限）+ exists_min_image；右支由正项和正性排除——窗口化界（Window.lean:26 反证形态）的数学基础
- **SmallClassNumbers 认知修正**：classNumber (Kstar 3) = 1 是引擎 Level-3 星型域的分类数平凡（非虚二次域类数问题）；eq_one（模 2 特征恒主）；MainTheoremsCritical = 最小层级/最小模退化特判层
- 解读系列新增：docs/walkthrough/14-Landau二分法本体.md；数学背景笔记 14（含术语核对方法论提醒）

## Kato 机器与 Taylor-Wiles 拼贴（第十五轮侦察补充）

- **词汇分布统计**：Kato 1071 文件 / patching 702 文件 / TaylorWilesObstructionBound 实名文件 / LiteratureResults/KatoEulerSystems 目录——**模性提升（R=T）全套现代机器入列**
- CorGKOf 装配链全读：litN 文献假设（OpenImage/galois_cohomology_from_literature）→ lemmaK → 非分歧自守性 → Kato 二重 W（katoTwoW_of_printsH）→ 刚性 I/II → 单特征酉 → U3.CorGK → 层级 3 界；patching 入口 = published_hypotheses_from_patching_alt
- **修正后的引擎成分表**：文献库 + Theta/Siegel-Weil + Poitou-Tate + Arakelov 高度 + **TW patching 模性提升** + **Kato Euler 系统** + 形式桥网络——完整现代朗兰兹武器库
- 两条腿会师：Poitou-Tate 记账规则 × Kato Euler 系统上界数值 = Sha/Selmer 窗口的文献级来源
- 解读系列新增：docs/walkthrough/15-Kato与TaylorWiles.md；数学背景笔记 15

## TW 障碍界与 Kato 定理直译（第十六轮侦察补充）

- **TaylorWilesObstructionBound 本体**（156 行）：Norm = TW 提升障碍界命题（注入有限提升 j + 行列式/特征相容 + N3/N4）；**CohP 结构体** = Poitou-Tate 性质包（lf/lt/le/gf/ge/gw GreenbergWiles/pt PoitouTateNormalised/tame）；**HidaSetting** 出场（Hida 族框架）
- **KatoLitO/KatoO 直译**（31 行）：Deligne 模性表示（∃ V 连续 ∧ FrobPoly）+ 非临界扭转（2r≠k）Selmer 有限性——**文献供"有限"，引擎供"多少"**的分工确认
- PT 机器三份正式化：Statement.lean（引擎侧）/ CohP（TW 侧）/ PoitouTateNormalised（文献侧）
- 解读系列新增：docs/walkthrough/16-TW障碍界与Kato定理直译.md；数学背景笔记 16

## Kstar 虚二次域舞台与 Jacobi 显式计算（第十七轮侦察补充）

- **Kstar p = Q(√−p)**（SplittingFieldIsoQuadratic.lean:51）：p≡3 mod 4，判别式 −p、全复、2 维、CM 域——**WinPair 素数 q 的用途实锤：造虚二次域舞台**
- Level-3 临界语义对齐：classNumber (Kstar 3) = 1 即 Q(√−3) 类数 1（Heegner 域）——解读 13 猜测半对
- **supplyOfAdmOf 中部**：Win 集合 = {x | ∃ Y q d e, WinDatum}（窗口数据显式记录）；常数链落地（hYA 幂次往返、hq3 排除 q=3、h4N）；**hjacb = 纯二次互反律计算**（p|d+1 ⇒ jacobiSym(−d,p)=1，d+1 小素因子全分裂——genus 理论实锤）
- GreenbergWiles 多源：GalCoh.lean:175 定义 + GreenbergWilesOfPoitouTate（EulerChar+Finite ⇒ GW）+ 文献版
- 解读系列新增：docs/walkthrough/17-Kstar虚二次域舞台.md；数学背景笔记 17

## 三区定性：高度消失/均方界/GL3 逆定理（第十八轮侦察补充）

- **HeightAndVanishing**（59 文件）：BchiFacts（Bernoulli 回归）、CM 2-adic 界、Count 计数族、GdOfHost/GdIffIndex（Gd 绑定宿主）、EtaKer、FinalLe/U——Kstar 类群与 Gd 量绑定到 Host 的判据区
- **MeanSquareBounds**（36 文件）：GaussSumFunctionEq（Gauss 和）、meanSqK 均方量、**pairEx = 好素数对存在定理**（pairEx_lift/box/g 三引理；QH.pairEx 出处）、CountBad/BadShare 坏份计数、kappa4loglog、Stage 阶段推进、SmallZeros
- **BlockDecomposition**（AutomorphicSpectrum）：ShintaniFormulaGL3Diag + ConverseTheoremConstantTerm（GL3 逆定理）——波的"自守户籍"登记
- 引擎区划总表（11 区）见解读 18
- 解读系列新增：docs/walkthrough/18-高度消失区与均方界.md；数学背景笔记 18

## 机器汇合点与小零点宝石（第十九轮侦察补充）

- **机器汇合**：pairEx_g 证 An.gChi = Gchi（Landau 复量 = 均方正项和）——Landau 机器与均方机器在对象层面汇合；**Gchi 精确定义定格**：Σ Λ(n)·χ(n)·max(y/n−1, 0)（ramp 权离散 Landau）
- log_exp_product_bounds：WinPair 上界（log q ≤ Y^(eps/5)、log d ≤ Y^(eps/5)·log²Y、3 系数、8M 与 mod 8）的推导出处
- **SmallZeros 全文**（47 行）：noExc_one（L(1,χ)≠0 + 连续性）→ noExc_level（固定模有限）→ small_zeros（对 N₀ 归纳取 min ⇒ 所有 N≤N₀ 非主特征在 (1−c₀,1) 一致无零）——Re≈1 处的兜底带，大小两层配合
- namespace QH（MeanSquareBounds 容器）语义待定
- 解读系列新增：docs/walkthrough/19-机器汇合点与小零点宝石.md；数学背景笔记 19

## thinH 整合定理与 ζ 通道证明体（第二十轮侦察补充）

- **thinH 全文**：SmallZeros(8B 层) 与 BoxW 的 1−1/400 宿主带取 min——**1/400 接口定谳**；level_dvd（N ∣ 宿主 condN，conductor_dvd_level）；分支 q|N ∨ d|N → BoxW 界，否则 Gauss 和等式 + SmallZeros——**ThinOK 条件本体 = 双保险零点控制**
- QH namespace = CharacterBoxes/ThinChoice.lean（薄选择体系）
- **Gz 应用群**：RiemannHypothesisOfPowerBound / GrowthBoundGivesRiemannHypothesis（条件主定理第三变体）/ FixedEpsilonConcreteGrowthBound；**ζ 通道证明体在 GlobalRankLatticeProofs/（ZetaZeroFreeRegion + LandauZeroFreeHalfPlane——全局秩格几何化）**
- L 函数因式分解架构：非本原 L = 本原 L × 欧拉因子；imprimitive 补齐引理自动传导（CritLine/KatoLitO 只需本原）
- 解读系列新增：docs/walkthrough/20-thinH整合定理.md；数学背景笔记 20

## G0 统一引理与 p-adic 世界（第二十一轮侦察补充）

- **gauss_sum_function_eq 真身**：An.gChi = G0 统一引理（QH 侧统一 G 函数；max 在支撑上退化）；isReal_of_sq 实特征引理——修正解读 18 初猜（非 tau 恒等式，Gauss 和机器在 thinH 下游）
- **ζ 通道三层结构**：GlobalSchurBounds/ZetaZeroFreeRegion（真身）→ GlobalRankLatticeProofs 薄适配（G_eq_Gz 命名空间桥 + PointsLemma）→ 条件主定理层；**命名空间桥接引理（X.Y = Z）是 AI 跨目录装配的逻辑焊点**（多例：An.gChi=Gchi、An.logDerivativeAtOne=G.T、G_eq_Gz）
- **GL3Theta 1013 行** = p-adic 多元幂级数层 GL3 Theta（Wp/InWf/IntegralW/logMv/SimeqW/tauK——tauK 即 Gauss 和的 p-adic 化身）；Theta 机器复解析与 p-adic 双轨确认
- 解读系列新增：docs/walkthrough/21-G0统一引理与padic世界.md；数学背景笔记 21

## Frobenius 读数与 Kudla 家族（第二十二轮侦察补充）

- **ZetaZeroFreeRegion 真身**（275 行）：Chr D 抽象特征（GG→Cˣ）、Unram（p∤宿主判别式）、InertK 惯性分类、**Reads（chi(p)=psi(Frob_p) 的 Artin 式对接）**、prim 选择公理选本原读出者、Gc/Lp 把 Landau 量提升到抽象层——抽象-具体对接完成
- **GL3Theta 尾部**：TwistedThetaTheorem → toTaylorLogMetric（对数量规）→ .rec 产出九条矩条件（vec22/th22/RelativeDeterminantEquation/int22/mom22/str22/famItems）；**IsDiscriminantTwelfthRootOfIdealLattice**（判别式十二次根格）；**KudlaFamilyStatement**（Theta 导数模性族化）——HeightAndVanishing 的引擎室
- 全链叙事闭环：Kstar 类群/判别式 → Theta 导数模性 → 宿主读数窗口 → VWin → PT 记账 → Chebyshev 截断 → Landau 判据 → EveryCharacter → RH
- 解读系列新增：docs/walkthrough/22-Frobenius读数与Kudla家族.md；数学背景笔记 22

## TwistedTheta 陈述解剖与 Weyl 维数（第二十三轮侦察补充）

- **TwistedThetaTheorem 陈述解剖**（928-953 行）：aux₃ = LatticeGrowthBound ∧ SplitModelProperties ∧ DeterminantCharacterProperties ∧ readW；Adm3s = admJ ∧ **InducedCMType** ∧ HostFieldConditions；Stmt := Adm3s → aux₃；ConclusionE = X 恒真版；.mono/.rec 组合器——**模性主定理的参数化形式**（C 可调结论强度、X 附加要求）
- **AdmittedWeylDimension**（151 行）：GAf 仿射群 + LevelData + ColRep 列表示的 **Weyl 维数容许界**（LevelDataRankBound/BaseWeightColumnCondition）——链绑定组合账本的保险丝
- InducedCMType：Kstar CM 型作为宿主体系对称性种子
- 解读系列新增：docs/walkthrough/23-TwistedTheta陈述与Weyl维数.md；数学背景笔记 23

## Greenberg-Wiles 本体与供给收口（第二十四轮侦察补充）

- **TwistedThetaTheorem 定义体**：对每曲线理想 cc/每判别根 δ/每特征 chi，存在 e: FamE 满足九条矩（vec22/th22(C)/**eq22(χ)**/int22/mom22/LSM/str22）+ famItems + X——特征化扭曲 Theta 模性
- **GreenbergWilesAt 本体**（GalCoh.lean:175）：前提 = PTShaAt 基数相等 + 有限性（Statement.lean 四假设的服务对象确认）；结论 = 带 Selmer/局部因子/实位因子的 Euler 示性数平衡式——**长度记账的文献级原件**
- **supplyOfAdmOf 尾部闭合**：hQS 预算 → hA 宿主实例化 → hprime（QS 素因子 ⊆ 2ψN）→ boundedTw 有界扭转 → isChiField 落地 → VVle mono → HostExW 输出——装配完整
- **主干侦察完成**：24 轮覆盖全部主区块，剩余边角（LinkGLOBAL7 层级表/GL3Θ↔GL4 梯子/GL3Θ 前 900 行 p-adic 细节）为技术性深化
- 解读系列新增：docs/walkthrough/24-GreenbergWiles本体与供给收口.md；数学背景笔记 24

## 提炼报告（第二十一轮）

- **docs/NEW-MATH.md 落盘**：新数学结构与工具提炼报告——方法级 4 项（窗口体系/宿主舞台/形式桥网络/桥接焊点）、对象级 4 项（抽象层级语言/LiteralAutomorphy/Host 家族/G 系列谱系）、定理级 2 项、工具级 3 项、常数体系 1 项；每项含实锤/推断置信度标注与经典对应物
- 侦察转向提炼与综合（边角深化按需）

## 供给收官与 LinkGLOBAL 定谳（第二十五轮侦察补充）

- **LinkGLOBAL 定谳**：参数化谓词族 LinkGLOBAL Fm Cabs CH C0 eD eL；LinkGLOBAL7 = 第 7 变体、Tied4 = 第 4 类绑定（版本化命名，非深奥常数）——定谳；配套测量词 TuSize/DGamSize/CoverAll/MuRank
- **supplyOfAdmOf 全验证收官**（135 行三段覆盖）：尾段 QS 预算链（nlinarith 簿记）→ 宿主实例化 → 素因子限制（l|QS ⇒ l|2ψN）→ boundedTw → IsChiField 落地 → VVle mono → HostExW 四元组输出——**装配完整闭合**
- "程序阅读法"总结：obtain 剥洋葱 / by_cases 分叉 / nlinarith 簿记 / mono 传递——导航 17M 行的四模式（解读 25 + 笔记 25）
- 解读系列新增：docs/walkthrough/25-供给装配线全验证.md；数学背景笔记 25

## 常数 7 定谳与 chiD 体系（第二十六轮侦察补充）

- **LinkGLOBALPk 条件清单**（56 行）：tVol 标准格绑定 / tOm 判别式十二次根+OmLink / tFree 薄自由 / **tTh ExistsTwelfthRootCharacterThetaFamily C22** / **t7 flipTwoThree.admF7** / tCV ColVal / t10 IncidenceTransport + s59/s22/s23/s24/s10/provedFourF/provedFiveF/hF3 编号命题库——**常数 7 终极定谳：flipTwoThree 容许族 7**（2-3 翻转体系）；链条 FamGL → linkGLOBAL_pk → LinkGLOBAL → TopG
- **GL3Theta 中段 chiD 体系**：类群特征赋值（代数整数单位/惰性位范数 1/幂方程 chiD^h = Π emb(z)^(-1)）+ **NormOnePowerPrincipal 类群主化** + powRatAll_of——**Kstar 虚二次域类群 = 读数体系的群论底座**（实锤）
- supplyOfAdmOf 三段全覆盖收官确认
- 解读系列新增：docs/walkthrough/26-常数7定谳与chiD体系.md；数学背景笔记 26

## flipTwoThree 翻转闭包与 admF 族（第二十七轮侦察补充）

- **flipTwoThree 语义定位**（CurveDVRSpecialization/FlipTwoThree.lean:38）：链接关系自反传递闭包中 2/3 素数的翻转保持——图论连通性代替逐点验证；层级链 flipTwoThree → admF7 → t7 → FamGL → LinkGLOBAL
- **admF 编号族**：admF5/admF7/admF9（VanishingOnXAndXPlusBranching 消失分支容许族序列）+ FlagMeasures/AmpBoundsUniform/LocalNongenericBoundRecord 配套 + **SiegelMassRatio**（mass 公式判别式根出处，解读 22 的经典原型）
- 解读系列新增：docs/walkthrough/27-翻转闭包与容许族.md；数学背景笔记 27

## GL3Theta 真身：椭圆曲线 p-adic 形式群（第二十八轮侦察补充）

- **G1 结构揭秘**（GL3Theta 68-105 行）：lam 嵌入 + abelian₂ 复格 + WeierstrassCurve 变量变换 + wq/ex 幂级数——**椭圆曲线的 p-adic 形式群图式**；W = C•wModel（p-adic 模型）、l = flog（**形式对数**）、ph = −logMv(ePhi1)（**CM 椭圆函数 log**）、be a b = 双线性偏差检验；At = 与宿主曲线理想/判别式根绑定
- **GL3Theta 在椭圆曲线 p-adic 形式群上运行 GL3 Theta**——Kstar CM 域经 ePhi1 获得几何实现（解读 17 的延伸）
- **双副本现象实锤**：gauss_sum_function_eq 两份私有副本证明体实质相同（tactic 风格微调）——AI 生成以模块自足换零耦合，冗余可压缩（对应 blueprint 的 -46.6%）
- **FamGL 五参数**：C0/eL/C3/**crystallineComparison（晶体比较常数）**/C22
- 解读系列新增：docs/walkthrough/28-椭圆曲线形式群.md；数学背景笔记 28

## GW 平衡式全形与 At 八推论（第二十九轮侦察补充）

- **GreenbergWilesAt 平衡式完整形式**：card(Sel(rho,L))·card(H0(rho*))·Π局部 H0·archH0Card = card(Sel(rho*,perpCond(L)))·card(H0(rho))·Π card(L v)——perpCond 正交对偶条件包；arch 实位因子
- **PT 正式化确认为四份**：Statement.lean（引擎侧 VFormula）/ CohP（TW 侧）/ PoitouTateNormalised（文献侧）/ GalCoh PT 假设区（LocalFiniteness/LocalTateDuality 全称包 + GreenbergWilesAt）——同一数学四种粒度
- **At 八推论**：GL3Theta 的形式群绑定谓词带八条推论（谓词-推论组织法）
- 解读系列新增：docs/walkthrough/29-GW平衡式全形与At八推论.md；数学背景笔记 29

## 下一步侦察队列

- [ ] GlobalTheory.GLq.Green 的定义与数学含义（引擎全局输入）
- [ ] UpperTheory.Top 全家：VWin / shapeWin / supplyChi / imprimitive
- [ ] Hyps / LinkN / DRS 假设系统的语义
- [ ] Formalism.HC.ZeroFreeAll 的内容（HC 是什么）
- [ ] Formalism 顶层 40+ 目录逐个定性，区分"标准数学形式化" vs "新工具"
