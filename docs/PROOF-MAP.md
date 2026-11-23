# 证明地形图（章节化 v2）

> 自顶向下追证明主干的语义地图。阅读约定：只读定理**声明**（数学内容），跳过证明体。逐轮详细记录见 docs/walkthrough/ 系列（37 篇），本图为其语义索引与精华浓缩。

## 1. 主线收束链（已闭合，全部人类可读）

- Main.lean（12 行）→ Supplements/Kernels/MainTheorems.lean（16 行）
- allChi : UpperTheory.EveryCharacter = UpperTheory.FinalTheorems.everyCharacter（引擎顶点，CharacterBoxes/EveryCharacter.lean:13）
- rhOfAll : RiemannHypothesis = Formalism.VW.rh_of_every allChi（Formalism/GammaFactorNonvanishing/CritLine.lean:29，32 行桥）
- critAll / claimAll：GRH 临界带版本（同走 critLine）
- 双装配通道：通道 A = CritLine 版（主线）；通道 B = MainConclusion → RiemannHypothesisOfEveryCharacter（完成函数对称版，解读 13）

**数学结构**：Hadamard–de la Vallée Poussin 反射法复活（Γ 因子非零 + 函数方程反射 + 模 1 退化），详见解读 01 与笔记 01。

## 2. 规模分布

| 库 | 行数 | 占比 | 角色 |
|---|---|---|---|
| Development | 12,232,663 | 70.4% | 朗兰兹机器全套 |
| Formalism | 3,200,748 | 18.4% | **形式桥网络 + 新工具家族** |
| GroundTheory(+Fields) | 1,119,138 | 6.4% | 基础理论 |
| ReciprocityTheory | 563,016 | 3.2% | 互反律 |
| CompanionTheory | 194,218 | 1.1% | 谱几何/Harish-Chandra/Eightfold |
| PositivityTheory | 55,130 | 0.3% | 正性理论 |
| Lemmata | 9,232 | 0.05% | 引理（意外地小）|

总声明 971,932；import 枢纽 top3 全在 Development.AbelianVarietyTheory.Definitions.Divisors。

## 3. 引擎区划总表（11 区）

| 区 | 位置 | 角色 | 解读 |
|---|---|---|---|
| 收束 | Supplements/Kernels | 28 行终局 | 01 |
| 经典桥 | Formalism/GammaFactorNonvanishing | 反射法 | 01 |
| 组装 | CharacterBoxes + UpperTheory.Top | Gm/供给/宿主 | 02/05/12 |
| 平方根截断图纸 | SharpRestriction 各区 | Chebyshev/Scales/Chain | 14/30/31 |
| Poitou-Tate | Formalism/GaloisCohomology + GalCoh | 长度记账 | 04/29 |
| 均方分析 | MeanSquareBounds | Gauss 和/pairEx/SmallZeros | 18/19 |
| 高度消失 | HeightAndVanishing | Kstar 类群/Bernoulli | 17/18 |
| 模性提升 | PatchingModules + ModularityArgument | TW/Kato | 15/16 |
| GL4 链接 | LocalToGlobal/GlobalTheory/GL4 | 分支链接族 | 22 |
| GL3 逆定理 | AutomorphicSpectrum/BlockDecomposition | Shintani/逆定理 | 18 |
| 文献 | Published 家族 | 接入层 | 02 |

## 4. 定谳事实清单（全部经源码验证）

### 常数角色表

| 常数 | 角色 |
|---|---|
| 401 | Sha 窗截断指数（VWinAt ψ 401）|
| 1/52 | eps 上限 |
| 3/2 | 覆盖指数 la（Scales）|
| 400 | 1 附近零点带宽（BoxW）|
| min(c₀s, 1/400) | thinH 整合带 |
| 15 | pde/pde' 模数（HostGood）|
| 7 | eD+eL+7 误差预算包 |
| eD/eL | 斜率引理族/斜率损失族指数（provedFourF/provedFiveF）|
| 1728 | j-不变量规范化（admJ：1728·g₂³ 代数整数性——CM 定理）|
| 7（LinkGLOBAL7）| flipTwoThree 容许族 7（2-3 翻转体系）|
| 2-3 翻转 | WinPair q≡3 mod 8 / d≡7 mod 16 对称分工 |

### 组件语义表

| 组件 | 语义 | 位置 |
|---|---|---|
| Gz | 主特征正项主项 Σ Λ(n)(y/n−1) | GzEq.lean |
| Gchi/Gm | 特征正项和 / 主项+加权波 | pairEx.lean:61, ExplicitFormulaErrorOfHostConditions:38 |
| 判据桥 | Gm ≤ y^θ 覆盖 ⇒ ZeroFreeAbove θ | 同上:41, Window.lean:31 |
| VVle/VWin/VLen/HypV | Sha 窗口四姐妹（V 同源）| Statement.lean/ExistsPageN |
| Host/HostGood | 五素数舞台 + 范数方程 π·conj(π)=g + 窄窗 | ThinScalesIffHostBound.lean |
| GLq.Green | 有限域 GL 标签-表示字典 | GreenCuspidal.lean:268 |
| rhoCh/lift_eqC | 列链特征 + 类群特征和（稳定子倒数加权除子级数）| GL3Theta 460-520 |
| Petersson 三件套 | 均方界文献级引擎室 | LocalQuadraticParts.lean |
| ChainTied | 换格算子链绑定（movesCompose 复合律）| TieGlobal.lean:97 |
| modelXi | 换格 sqrt(volP) 缩放 | GL3Theta 700-780 |
| wCocycle（c²=kap）| Weil 投影表示 2-上循环 | GL3Theta 750+ |
| LiftObj/IsKer | Q̄ 系数有限组合 + p-adic 积分 + 特殊素数集 S | GL3Theta 521-600 |
| admJ | 1728·g₂³ 代数整数性（CM j 定理）| GL3Theta 835 |
| GreenbergWilesAt | Selmer Euler 示性数平衡式 | GalCoh.lean:175 |
| PT 四份正式化 | Statement/CohP/Normalised/GalCoh 包 | 各处 |

### 证明链环（34 轮闭环）

素数对 → Kstar 虚二次域（Q(√−q)，genus 透明）→ chiD 类群特征赋值（NormOnePowerPrincipal 主化）→ TwistedThetaTheorem 模性（Kudla 矩条件，At 八推论：立方检验群/beBiadd/积分性/phNorm）→ LChain + lift_eqC 特征和 → 宿主读数窗口 → VWin Sha 窗口 → Poitou-Tate 记账（VFormula + GreenbergWilesAt 平衡式）→ Kato 有限性（文献）→ 切比雪夫平方根截断 → Scales la=3/2 覆盖 → 链绑定 → Landau 判据（真空半径/实点排除）→ EveryCharacter → VW 桥 → RH

## 5. 新数学结构与工具

详见 docs/NEW-MATH.md（方法级 4 / 对象级 4 / 定理级 2 / 工具级 3 / 常数体系）。核心：UpperTheory 窗口体系、宿主化架构、形式桥网络、G 系列量谱系、LiteralAutomorphy 离散编码、【推断】Host 数字家族。

## 6. 逐轮日志索引

| 轮 | walkthrough | 主题 |
|---|---|---|
| 01 | 01-主线收束链 | 门面/声明/收束/桥 |
| 02 | 02-引擎深潜 | 文献库/WeilBound/TopPlug/装配线 |
| 03 | 03-窗口不等式与Green字典 | VWin 解剖/素数对/IsChiField/Sha 界 |
| 04 | 04-PoitouTate引擎 | LData/VFormula/Selmer |
| 05 | 05-Host舞台 | HostGood 十四条/GChi 要求 |
| 06 | 06-放大机制 | Scales 3-2/Chebyshev/链绑定 |
| 07 | 07-平方根截断与Landau判据 | 核心不等式/判据层 |
| 08 | 08-显式公式函数Gm与窗口判据 | Gm 定义/判据桥/供给收官 |
| 09 | 09-Gz主项与族连通 | Gz 闭式/FamilyClassConnected/HypV |
| 10 | 10-条件主定理双璧 | LandauZeroFree/PowerBound/组织学 |
| 11 | 11-RhOfRight反射封口 | ζ 通道/SchurBounds 定性 |
| 12 | 12-装配主车间与Landau工具箱 | 配料清单/Landau 九件套/GL4 |
| 13 | 13-双装配通道与类数三临界 | 通道 B/SmallClassNumbers |
| 14 | 14-Landau二分法本体 | 真空半径/实点排除/Level-3 修正 |
| 15 | 15-Kato与TaylorWiles | 词汇分布 1071/702 |
| 16 | 16-TW障碍界与Kato定理直译 | Norm/CohP/KatoLitO |
| 17 | 17-Kstar虚二次域舞台 | Q(√−q)/hjacb 互反律计算 |
| 18 | 18-高度消失区与均方界 | 三区定性 |
| 19 | 19-机器汇合点与小零点 | gChi=Gchi/SmallZeros |
| 20 | 20-thinH整合定理 | 1/400 接口/导子水平 |
| 21 | 21-G0统一引理与padic世界 | G0 统一/三层适配 |
| 22 | 22-Frobenius读数与Kudla家族 | Reads 对接/Kudla 矩条件 |
| 23 | 23-TwistedTheta陈述与Weyl维数 | aux₃/Adm3s/Stmt/Weyl |
| 24 | 24-GreenbergWiles本体与供给收口 | 平衡式/装配闭合 |
| 25 | 25-供给装配线全验证 | LinkGLOBAL 定谳/程序阅读法 |
| 26 | 26-常数7定谳与chiD体系 | admF7/类群主化 |
| 27 | 27-翻转闭包与容许族 | ReflTransGen/Siegel mass |
| 28 | 28-椭圆曲线形式群 | G1/flog/ePhi1/CM |
| 29 | 29-GW平衡式全形与At八推论 | perpCond/四份 PT/谓词推论法 |
| 30 | 30-At八推论全解与FamGL槽位 | 立方检验群/eD eL 出处/Kudla 三份 |
| 31 | 31-斜率族定位与深嵌套观察 | LocalQuadraticParts/23 层投影 |
| 32 | 32-列链特征与Petersson界 | rhoCh/lift_eqC/Petersson |
| 33 | 33-LiftObj与IsKer证明本体 | 代数系数/p-adic 积分/主化 |
| 34 | 34-Weil表示换格链与2-上循环 | sqrt(volP) 链/wCocycle |
| 35 | 35-j不变量1728与Xi公式族 | admJ/PhiHat/xiOne/xiMove |
| 36 | 36-RelDetPinned生态与二十接口族 | 生态闭环/二十接口 |
| 37 | 37-RelDetPinned证明链与RS机器 | 大定理/RS 球形机器 |

## 相位函数理论栈（第三十八轮侦察补充）

- **PhIsotropic**【消失机制完全体】：迷向组（hP 全零）+ Primitive ⇒ **PhOn ≃ 0**（相位级数完全消失）——HeightAndVanishing 的数学引擎
- **PhUnitary**：正交系 ⇒ PhOn 可加分离；**PhDual + DualIso + beSum**：互双正交对 ⇒ 对偶分解
- **jetsPh**：p ≠ d ⇒ 整数；**p = d ⇒ ‖jetPh 2‖ ≤ √p**（平方根截断在相位射流层再现；临界例外与 Kato 2r ≠ k 同构）
- **atTwo**：2-挠点真奇性（log 消失但增长率超几何）——素数 2 特殊性定谳（需宿主素数对单独处理）
- 解读系列新增：docs/walkthrough/38-相位函数理论栈.md；数学背景笔记 38

## GL3Theta 完整理论栈 16 层（第三十九轮侦察补充）

- **GL3Theta 文件身份终定**：CM 形式群上的 Weil 相位理论完整栈（1013 行 16 层）——形式群/绑定/Jacobi 分类/模型存在/立方/双线性/积分/CM 规范/共轭/**分裂消失**/对角/射流/Taylor 化身/挠点/Weil 算子/族化
- **关键公式**：CM 相对范数缩放（phAt(mulBy α.1 Xv) ≃ N(α)·phAt(Xv)，N(α) = α.1·α.2）；**分裂消失**（SplitK ⇒ be ≃ 0 ∧ ph ≃ 0）；对角关系（be(Xv,Xv) ≃ 2·ph）；**ser1/atU Taylor p-adic 化身**（iteratedDeriv n G 0 / n! 经 lam → 形式对数代入）
- **素数三分类机制**：分裂位消失 / 惰性位 ModelOverW / 分歧位 √p 收缩
- **IsTwoTorsionPointUnkilled**：CM 杀伤测试（(1+i√d)/2 平移不抹掉）——2-挠真奇性判据
- U1 底层定义待溯（imports 深处：FiltrationBoundaryCriterion/CocycleLiftCriterion/ParConsts）
- 解读系列新增：docs/walkthrough/39-GL3Theta完整理论栈.md；数学背景笔记 39

## U1/IsTheta0 定谳与 aux₃ 45 条量规（第四十轮侦察补充）

- **al1 平移符号因子**：(−1)^round(√d/2·|x|²/area)——虚二次域二次型的 Gauss 相位（解读 34 (−1)^m 的格平移层实现）
- **IsTheta0**：全纯 + 平移关系 + G(0)=1——Theta 良构谓词；**normSq1** = exp(−π|z|²/area) 加权 L² 积分（Theta 核）
- **thPow 幂公式**：normSq = normSq1^(fF·N·N')——**矩条件指数 = 维数乘积**（Weil 表示张量积结构）
- **famItems 五件套**：intOrtho/intHyp/prim/kerComb/**thPow**
- **aux₃ = 45 条合取对数量规包**（LatticeGrowthBound 26 + SplitModelProperties 16 + DetChar 3）；Stmt = Adm3s(3) → aux₃(45)——「3 条容许换 45 条量规」复利式结构
- 新词汇登记 14 项（phW/isoF/endIntW/beW/PhDualW/modelShort/phEven/beGc/okpInert/supH/iopUnitary/repEx/detIdP/repExS）
- 解读系列新增：docs/walkthrough/40-U1定谳与45条对数量规.md；数学背景笔记 40

## fF 定谳与新词汇定性（第四十一轮侦察补充，轻量）

- **fF 定谳**：fF = finrank Q F = **宿主域次数 [F:Q]**（SiegelMassRatios/MassRatio.lean:19——质量比率维数参数）；thPow 幂公式 = normSq1^([F:Q]·N·N')——域次数 × 格维数记账
- **phW/beW 定谳**：Frobenius 纤维曲线版相位族（FrobeniusFibreCurves/StatementW.lean——与 p-adic 形式群 G1 平行的第二实现）
- 其余新词汇归入 GL3Theta/SizeWindowBrackets 接口族（语义按名可推）
- **新词汇定性完成宣言**：40 轮全部新词汇已定性
- 解读系列新增：docs/walkthrough/41-fF定谳与新词汇定性.md；数学背景笔记 41

## 7. 下一步侦察队列（低优先边角，按需）

- [ ] LinkGLOBALPk FamGL 后续字段（s 系列之外的槽位）
- [ ] GL3Theta 前 900 行 p-adic 细节逐段
- [ ] gauss_sum_function_eq 双副本逐行 diff
- [ ] U(T,t,e) 基础函数定义
- [ ] TwistedThetaTheorem 主定理证明体（rec 输入构造）
- [ ] Petersson 界引用链下游（PointPropertyEqSizeFree/FreeFamilyOfLeaves）
- [ ] rhoThree 供给链（sSharp 嵌入公式证明）

## 8. 已完成里程碑

- [x] 主线收束链闭合（01）
- [x] 引擎顶点 EveryCharacter 组装配方（02/05）
- [x] 窗口不等式四层解剖（03）
- [x] Poitou-Tate 记账引擎（04）
- [x] 宿主舞台设计（05）
- [x] 放大机制与链身份（06/14/34）
- [x] 平方根截断与 Landau 判据（07/08）
- [x] 常数全定谳（26/35 等）
- [x] 供给装配线全验证（25）
- [x] 模性提升机器入列（15/16）
- [x] 新数学结构提炼（NEW-MATH.md）
- [x] 证明总览合成（PROOF-OVERVIEW.md）
