# 解读 04 — 引擎核心：LData 与 Poitou-Tate 长度公式

> 对应第四轮侦察。Formalism/GaloisCohomology/Statement.lean（186 行）是引擎的数学心脏，本篇全文解剖。

## 1. LData：分圆 Galois 场景的打包

structure LData (F Ω l) 四件套：

- S：F 的高度一位素点中 l 以上的有限集（hS : S = Above F l）
- A：每个 v ∈ S 在代数闭包 Ω 中的位提升（ValuationSubring）
- chi：S-分支 Galois 群 → Z_l 单位的特征，且 hchi 钉死 chi = 分圆 l-adic 特征 cycZ
- （QZ l := Q_l / Z_l —— 离散挠系数群）

⇒ LData = "数域 F 在素数 l 处的分圆 Galois 表示场景"。IsChiField 构造的每一个数域 E（解读 03）配每个素数 l 就是一个 LData。

## 2. Tate 扭转与上同调

- qzTw D e：Q_l/Z_l 用 chi^(-e) 做乘法扭转 —— 分圆扭转 Q_l/Z_l(1−e)
- zlTw D n：Z_l 用 chi^n 扭转 —— Z_l(n)
- Sha D e := H¹(qzTw D e) 的全局-局部限制核 —— **真正的 Tate-Shafarevich 群**（对分圆扭转）
- shaLen D e := Z_l-模长度(Sha D e)（取值 ℕ∞）—— Sha 的 l-adic 对数
- VLen D e := Z_l-模长度(H²(zlTw D (e+1))) —— 局部不变量侧长度

## 3. Poitou-Tate 骨架（四条假设 + 一条公式）

- PTCokerAt：coker(全局 H² → Π局部 H²) 的长度 = H⁰(Q_l/Z_l(e)) 长度
- PTShaAt：Sha²(Z_l(e+1)) 长度 = shaLen(e)（两组 Sha 长度对偶相等）
- TateLocalDualityH2AtPlaces：局部 Tate 对偶 length H²(loc) = length H⁰(loc)
- GlobalH0TwistFiniteLength / LocalH0TwistFiniteLength：e ≠ 0 时 H⁰ 有限
- **VFormula**：VLen + length H⁰(Q_l/Z_l(e)) = shaLen + Σ局部H⁰长度 —— **长度恒等式**

⇒ VWin 的 V 与 VLen/VFormula 的 V 同源：窗口不等式度量并约束的正是 Poitou-Tate 长度平衡中的量。三个魔法常数（401 / 1/52 / 3/2）应当都是扭转指数 e 与窗口几何的参数化界（来历待查证，不再猜测）。

## 4. Selmer 框架与不变性

- unrAt：非分歧局部条件子模块；bkCond：按位分派条件（l 位用给定 Ll、Sig 位全放行 ⊤、其余位非分歧）
- SelAll / selLen：满足局部条件的 H¹ 子群 = Selmer 群及其长度
- InfUnram：无限位不分歧 + 全局 H¹ → 全 Galois H¹ 的单射性与象刻画
- Indep：shaLen / VLen / Σ局部H⁰ 与 LData 具体选取无关 —— 长度是场景不变量
- LDataExists：场景非空存在性

## 5. 引擎完整故事线（当前理解快照）

1. 素数对 (q,d) + 特征 ψ 切出分圈子域 E（IsChiField，解读 03）
2. 对 (E, l) 读出 LData：分圆扭转的 Galois 上同调
3. VFormula + Poitou-Tate 假设 ⇒ Sha 长度与 Selmer 长度的精确平衡
4. Selmer 长度可由解析侧（Theta/Eisenstein/Green 字典）估计 ⇒ VVle 的指数界
5. 显式公式（ExplicitFormulaError 家族）把 Sha 界翻译为 L 函数右半带非零
6. EveryCharacter → VW 桥 → RH（解读 01）

第 4 步"解析侧如何估计 Selmer 长度"是当前最大的未解缺口——这是下一轮侦察方向（shapeWin : Green → TopShape 已定位在 CharacterBoxes/ShapeWin.lean:27，supplyChi 在 SupplyChi.lean:8）。

## 6. 悬而未决

- shapeWin 的证明体（Green 字典如何产出 TopShape）
- supplyChi 的输入输出（窗口 VWin 如何逐特征供给）
- Formalism.HC（PrimeDiscriminants：RamDiscr / CycImage / SmallRam / HostRaw）——零点自由性的宿主层
- HostWW / HostOfField 的 Host 概念
- VFormula 的证明归属：它自身被证明了吗？还是 Published 输入？（存疑，待查引用链）

