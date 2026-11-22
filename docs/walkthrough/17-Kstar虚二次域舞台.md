# 解读 17 — Kstar p = Q(√−p)：虚二次域舞台与 Jacobi 显式计算

> 对应第十七轮侦察。WinPair 素数对的用途终极解答 + 供给装配线的实推理 + GreenbergWiles 多源定位。

## 1. Kstar p = Q(√−p)：虚二次域舞台（SplittingFieldIsoQuadratic.lean:51-55）

对素数 p ≡ 3 (mod 4)：**Kstar p 是 X² + p 的分裂域**，即 Q(√−p)，且：

- 判别式 discr = −p（最小判别式的虚二次域！）
- 全复（IsTotallyComplex）、Q-维数 = 2
- 存在 s ∈ Kstar p 使 s² = −p

⇒ **WinPair 的素数 q ≡ 3 (mod 8) 的用途实锤：构造虚二次域 Q(√−q)**。q ≡ 3 (mod 8) ⊂ q ≡ 3 (mod 4) 保证 −q 是基本判别式（genus 数最小）。配套词汇落位：CMFieldExponentialBounds（Q(√−p) 是最低级 CM 域）、HeightAndVanishing/KstarRam（Kstar 的分歧集）、TwoPrimeField（Q(√−q) 与素数 d 的组合 = "两素数域"）。

**KstarRam.lean / BchiFacts.lean（classNumber_pos of Kstar）**：Kstar 的类数为正、其类群参与"高度与消失"（HeightAndVanishing）论证——Level-3 临界件的 classNumber (Kstar 3) = 1 语义对齐：Q(√−3) 的类数恰为 1（九个 Heegner 域之一）！**解读 13 的猜测意外地半对了**：classNumber 确实是虚二次域类数，不过是引擎自己构造的 Kstar 层域的类数。

## 2. supplyOfAdmOf 中部：装配实推理（50-100 行）

- 窗口集合 Win 显式构造：{x | ∃ Y q d e, WinDatum ψ eps J c x Y q d e}——**WinDatum 记录每扇窗口的 (Y, q, d, e) 数据**
- 常数链落地：hYA（A ≤ Y，经 A = (A^J)^(1/J) 幂次往返）、hYK（K ≤ Y^(eps/5)）、hq3（**排除 q = 3**：log 3 ≤ 2 破坏 log q 下界）、h4N（4·ψ.N ≤ ⌊Y^(eps/5)⌋）
- **hjacb：纯二次互反律计算**——对 p ≠ 2、p ≤ Y^(eps/5)：p | d+1 ⇒ −d ≡ 1 (mod p) ⇒ JacobiSym(−d, p) = (1/p) = 1
  即：**d+1 的所有小素因子都是 Q(√−d) 的分裂数**（genus 理论实锤：d ≡ 7 mod 16 使 −d 的 genus 类确定）
- 随后 fieldChi 实例化（Frame φ、HostAx H0、QS | lcm(2^(e+2), M)）、admissible 拿 R

## 3. GreenbergWiles 多源定位

- 定义：ReciprocityTheory/Hypotheses/GalCoh.lean:175 GreenbergWilesAt（PT 侧）
- 证明三源：GreenbergWilesOfPoitouTate（**LocalEulerChar + LocalFiniteness ⇒ GW**——从 PT 推出）、greenberg_wiles_of_literature / of_open（文献版）

## 4. 悬而未决（缩小）

- Gm/Lm 在 Level 内的互逆关系（GzEq 已给主项；特征侧 Gm 的精确级数待最后确认）
- GL3Theta ↔ GL4 梯子抽样
- supplyOfAdmOf 尾部（100 行后）

## 下一步侦察队列

- [ ] HeightAndVanishing 目录定性（高度与消失——Kstar 类群的角色）
- [ ] GL3Theta 抽样
- [ ] QH.pairEx（MeanSquareBounds.pairEx——均方界！新线索）

