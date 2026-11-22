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

## 下一步侦察队列

- [ ] GlobalTheory.GLq.Green 的定义与数学含义（引擎全局输入）
- [ ] UpperTheory.Top 全家：VWin / shapeWin / supplyChi / imprimitive
- [ ] Hyps / LinkN / DRS 假设系统的语义
- [ ] Formalism.HC.ZeroFreeAll 的内容（HC 是什么）
- [ ] Formalism 顶层 40+ 目录逐个定性，区分"标准数学形式化" vs "新工具"
