# 解读 03 — 窗口不等式解剖：素数对、Sha 界与标签-表示字典

> 对应第三轮侦察。三个发现：窗口不等式的完整数学结构、Green 定理 = 有限域表示的标签字典、引擎的 Brauer 类群塔指纹。

## 1. VWin 的四层结构（CharacterBoxes/ExistsPageN.lean）

窗口不等式从外到内四层嵌套：

1. **VWin := ∀ ψ, VWinAt ψ 401** —— 每个素特征一个窗口；401 是截断指数常数
2. **VWinAt ψ Ct**：∀ eps ∈ (0, 1/52)，∀ 页码函数 e(x)（PageN：2^e 与 x^(2+8·eps) 同数量级），任取大 X，∃ J ≥ 1，∀ X ≥ X0，∀ 素数对 (q,d) 满足 WinPair eps X^(1/J)，∃ Y ∈ [X^(1/J), √X]，使窗口 [Y, Y²] 内处处 VAt
3. **VAt ψ eps Ct q d e x**：∀ 数域 E，IsChiField ψ e q d E ⇒ VVle E ⌊x^Ct⌋ e^(x^eps/2)
4. **VVle E t B**：E 的 Galois 上同调数据 LData 满足 (a) Sha 长度处处有限（≠ ⊤），(b) 任意素数集 S 上 Σ_{l∈S} log l · Σ_{e<t} shaLen(l,e) ≤ B

⇒ 窗口不等式的数学含义：**在几何级数推进的窗口 [Y, Y²] 内，每个特征的"关联数域"的 Sha 长度加权指数和被 e^(x^eps/2) 压住**。

## 2. WinPair：一对精心构造的素数

WinPair eps Y q d 的九条要求（全部显式）：

- q 素数且 q ≡ 3 (mod 8)；d 素数且 d ≡ 7 (mod 16)
- log q 与 log d 都在 Y^(eps/5) 尺度上（带常数 1/2 与 (log Y)²）
- q ∣ d + 1；且 d+1 的小素因子（≤ Y^(eps/5)）只有 2 和 q

这是引擎的"调音叉"：两个素数的模 8/模 16 余律、比例关系、以及 d+1 的光滑性被同时钉住。模 2 幂次的余数约束与 BoundAtTwoAndThreeForFamily 呼应——**2 与 3 的踪迹在这里就是 mod 8 与 mod 16**（另见 Jacobi 符号）。

## 3. IsChiField：特征的 Galois 固定域判据

IsChiField ψ e q d E：E 嵌入 2^(e+2) 阶分圆域 Q(ζ_N)，N 同时被 2^(e+2)、ψ 的模、q、d 整除；且 Galois 判据：

Galo(Q(ζ_N)/Q) 中固定 E 的元素恰为满足 [a ≡ ±1 (mod 2^(e+2))] ∧ [ψ(a)=1] ∧ [(a/q)=1] ∧ [(a/d)=1] 的 a

即 **E = 由特征 ψ、模 2 幂次、以及 q、d 的 Jacobi 特征联合切出的子域**。素数对 (q,d) 与特征 ψ 在一个分圆塔里"编码"出一个数域，引擎在那里读 Sha。

## 4. Green 定理：标签 → 表示的字典（GreenCuspidal.lean:268）

GlobalTheory.GLq.Green 是 ∀ 素数 p、标签数据 L、维度 d 的命题。证明骨架：

- GreenAll.cuspParam_all 给出 (hA, hB, hC)：尖参数三件套（唯一性、存在性、覆盖）
- 对每个素标签多项式 P（IsPrimeLab d P），选一个表示 σ P
- 构造字典 rep : (ZMod p)[X] → Gn p d → ℂ，P ↦ 特征(σ P)
- 三条性质：尖表示特征非平凡且为单位特征；特征相同 ⇒ 标签相同（唯一性）；每个尖表示的特征都命中字典

⇒ **GLq.Green = 有限域 GL_d(F_p) 的"标签-表示字典"全面成立**：尖表示的集合被素多项式标签参数化。这不是分析里的 Green 函数（拉普拉斯逆核），而是表示论的"标签/Greenberg 式"参数化——Alpöge 的个人命名法。命名家族：LabelDatum / LabelConv / HasCuspLabel / GreenCuspLabels，namespace PositivityTheory.GreenCharacters。

## 5. 引擎宏观图景（更新）

- Brauer 类群塔指纹：窗口不等式控制的是 **Tate-Shafarevich 型长度（shaLen）的指数加权和**。经典 Brauer 方法：类群塔 + zeta residue ⇒ 数域族的正性/非零性。本证明将其升级为：**显式素数对构造分圆塔 → Sha 长度指数界 → 特征的窗口估计 → L 非零**（与 Formalism 里 ExplicitFormulaErrorOfHostConditions、TotientGaloisClasses、RamificationFrobenius 完全吻合）
- LData 定义于 Formalism/GaloisCohomology/Statement.lean:54（structure），shaLen : ℕ → ℕ → ℚ（DataRows.lean）——**"Sha 长度"被离散化为行数据的有理函数**，这正是"数字-字母-行-列"语言的角色：把类群塔的组合结构编码为可乘的行表
- Formalism.HC 命名空间驻扎在 PrimeDiscriminants（素判别式、RamDiscr、CycImage）——HC（Harish-Chandra?）与"宿主"（HostWW/HostRaw）概念绑定，待解剖

## 6. 悬而未决

- LData/shaLen 的精确定义（GaloisCohomology/Statement.lean:54 下一步必读）
- VWin ⇒ EveryCharacter 的"形状供给"环节（shapeWin / supplyChi 的定义）
- 1/52 与 401 与 3/2 三个常数的来历
- Host（宿主）概念家族

