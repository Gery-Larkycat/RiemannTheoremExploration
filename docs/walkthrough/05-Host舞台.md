# 解读 05 — Host 舞台：每个特征一座剧场

> 对应第五轮侦察。Host（宿主）概念家族全解剖——它是引擎给每个 Dirichlet 特征量身搭建的"剧场"。

## 1. 类型系统：函数式要求

- HostReq : Type 1 := ℝ → Scale → ∀ R : Ranks, Host R → ℕ → Prop —— 宿主要求
- FReq : Type 1 := ∀ (Scale) (Frame) (HostAx) (Finset φ.A) (ℕ), Prop —— 特征要求
- 两者都是 Type 1 的"要求函数"：输入尺度/框架/宿主，输出命题。整个组装层是**命题级依赖注入**。

## 2. HostGood：宿主的十四条合格标准（ThinScalesIffHostBound.lean）

HostGood s C8 C5 c6 Cb H q0 要求宿主 H（数域 E 及其附属数据）满足：

1. HostVal / HostArith —— 数值与算术基本盘
2. secondSet_card_lower_bound、4·Lw·T2.card ≤ R.n0 —— 组合计数控制
3. QDq —— q、d 与尺度的相容（对应 WinPair 的素数对）
4. BoxW s H —— **窗口盒**（见第 4 节）
5. |dlogH H| ≤ s.x^s.eps —— 宿主的"对数导数"指数级小
6. ThinOK / BadOK —— 薄度与坏集控制
7. 分圆范数集合 BB(R.r, g 0) 与 BB(R.r, g 1) 不交 —— 两条水平线分离
8. **范数方程**：∃ π ∈ 𝓞_E，π·conj(π) = g_i 且 (π−1) ∈ 理想⟨QS·q·d⟩ —— 素数 g_i 是共轭范数，且 π ≡ 1 (mod QS·q·d)
9. pde、pde' ≡ 1 (mod lcm(15, QS·q·d)) —— **两个特殊素数对 15 的模**（3/2 阈值与 15 的家族嫌疑 +1）
10. q0 素数 ≡ 1 (mod QS·q·d)，大小 ≤ (QS·q·d)^C8
11. levelPrimes = {g 0, g 1, pde, pde', q0} —— 恰好五个"层素数"构成的仪表盘

## 3. GChi：特征 ψ 的两点要求（Supply.lean:42）

GChi ψ : FReq := fun s H TT t => EAtH (Level.cyc ψ) H TT s.x s.eps 4 ∧ VVle H.E t (√s.b)

即：**ψ 的要求 = 在宿主 E 中 ψ 有循环实现（EAtH，参数 4）∧ 宿主域 E 的 Sha 窗口很小（VVle）**。

supplyChi 的闭合：VWinAt ψ 401 ⇒ HostExW (3/2) (GChi ψ).req —— Sha 窗口（Poitou-Tate 侧）换来了"存在满足两点要求的宿主"。

## 4. BoxW.real_ne_zero：引擎的零点输出端（400 常数）

theorem BoxW.real_ne_zero ... (hβ : 1 − 1/400 < β) : LFunction χ β ≠ 0

**在宿主上生活的特征 χ（H.IsCharE），其 L 函数在实部 β > 1 − 1/400 处无零点**。400 是"离 1 有多远就能保证非零"的带宽常数；401 是 VWin 的截断指数——两者构成常数网（另与 1/52、3/2、15 关联，精确_roles 待后续定量核对）。

## 5. 组装总装线（全链闭合）

- shapeWin : GLq.Green → TopShape True True (Closed∘LinkN) TopG —— 字典产出形状（GlobalInterpolation 的 Link* 家族是"链接网络"机制）
- TopG : ∀ la > 1, ∀ G : FReq, HostExW la G.req ⇒ FamilyClassConnected (G.cls la) —— **从"每个特征有宿主"到"特征族连通"**
- zeroFreeAll_of_topG (hla : 1 < la) (TopG) (∀ψ HostExW la) : ZeroFreeAll —— 总装（内部经 zeroFreeOn_of_tiedWin_cyc + ChainTied 链绑定）

supply 链：VWinAt ψ 401 →[supplyChi/supplyOfAdm/admissibleClassesTwistedChar] HostExW (3/2) (GChi ψ).req。

## 6. 本轮数学解读（假设级，待源码验证）

Host 的语义：**为每个 ψ 定制的数域舞台**——ψ 在舞台上循环化（EAtH），舞台的 Sha 便宜（VVle），舞台有五素数仪表盘与范数方程保证的完全分裂结构（HostGood）。BoxW 给出"舞台上的 L 函数在 1−1/400 以右无零点"。ThinScalesIffHostBound（薄尺度 ⟺ 宿主界）暗示：**宿主界沿尺度序列 Scales la 逐步"推薄"**，la > 1（取 3/2）时薄化收敛到目标带，从而零点自由性从 β > 1−1/400 被推进到整个右半带——这是从"局部条带非零"到"全右半带非零"的放大机制（具体放大定理：ZeroFreeOn/zeroFreeOn_of_tiedWin_cyc，待解剖）。

## 7. 悬而未决

- zeroFreeOn_of_tiedWin_cyc：薄化放大定理本体（ChainTied 链绑定语义）
- Scales la / Scale 结构（尺度几何：s.x、s.eps、s.a、s.b、s.delta1…）
- EAtH / Level.cyc ψ / HostAx / Frame 的精确定义
- GlobalInterpolation Link*（LinkEx/G/Eta/Gl/Alt/Brest/WireSel）链接网络
- 常数网定量 roles：401 vs 400 vs 1/52 vs 3/2 vs 15

