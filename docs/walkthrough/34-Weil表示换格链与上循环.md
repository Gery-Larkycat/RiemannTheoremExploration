# 解读 34 — Weil 表示 p-adic 理论：换格链与 2-上循环

> 对应第三十四轮侦察。GL3Theta 700-780 行——ChainTied 之"链"的数学身份定谳。

## 1. 换格公式 modelXi：sqrt(volP) 缩放律

modelXi：对每条曲线理想 cc、判别式根 delta、每对 admitted 格（L0, L0'）、每个分裂位 P、每条 Theta 级数 th：

存在线性算子 Xi（C_p 矩阵函数 → VC 函数），使得：

- Xi(YP 的指示函数 1) = th（**Theta 值 = 算子作用于指示函数**）
- 换格时（EqOff 相容格 L, L'）：Iop算子(th) 的值按 **1/sqrt(volP(YP(L0,L0'), YP(L,L')))** 缩放

volP = 格指标比：(Y₀.addSubgroupOf Y₁).index / (Y₁.addSubgroupOf Y₀).index

⇒ **这是 Weil 表示的经典"换格公式"**：Theta 级数随格变化的缩放因子是格指标比的开方——Siegel-Weil 理论的标准现象（解读 02）在此的 p-adic 级实现。

## 2. movesCompose：链复合律——"链"的身份定谳

movesCompose：Iop(L2,L3) ∘ Iop(L1,L2) = Iop(L1,L3)（在 EqOffSplit 相容链上）

⇒ **换格算子可复合成链**——ChainTied/链绑定的"链"就是**换格算子链**！解读 14"链绑定"的数学身份：格链上的 Weil 表示算子复合。链绑定的作用：让"单格性质"沿链传导为"整条格链的性质"。

## 3. Weil 相位函数三件套

- **InLaP**：p^k · x ∈ La（x 是 p-adic 逼近格点）
- **wPhase**：p^k · qH(x) = m ∈ Z ⇒ **wPh(p, x) = (−1)^m**（qH = 二次型；**Weil 相位 = 二次 Gauss 和的符号**——经典 Weil 表示理论的核心公式！）
- wOnLattice：格上 wPh = al（格点处相位 = 代数量）
- **wCocycle**：Wop(x) ∘ Wop(y) = c · Wop(x+y)，其中 **c^(p^k) = 1 且 c² = kap(x,y)**——**Weil 投影表示的 2-上循环**（kap = cocycle，投影表示的障碍因子——Weil 表示不是真表示而是投影表示的标志）

⇒ **Weil 表示不是真表示而是投影表示**（差一个 2-上循环 kap）——这是 Theta 理论"符号歧义"的根源，也是需要"手工素数对"（mod 8/16 条件）来钉死相位的原因！

## 4. PhiHat：p-adic 局部常函数

PhiHat 用 LocallyConstant(Fin r → Z_p, C)——**p-adic 局部常函数 = Schwartz-Bruhat 函数的 p-adic 侧**（解读 02 的 Schwartz-Bruhat 控制函数在此的 p-adic 实现）。

## 5. 本轮结论（重大）

GL3Theta 的证明本体 = **Weil 表示 p-adic 理论的完整形式化**：换格公式（sqrt(volP) 缩放）+ 链复合律 + 相位函数（(−1)^m）+ 2-上循环（kap）+ 局部常函数。**引擎的"链绑定" = Weil 投影表示在格链上的相容性**——素数对的 mod 8/16 条件钉死 2-上循环的符号歧义。

## 下一步侦察队列

- [ ] PhiHat 后续（520-700 行——局部常函数到 Theta 构造的桥）
- [ ] qH/wPh/kap/al 的定义本体
- [ ] LinkGLOBALPk FamGL 后续字段

