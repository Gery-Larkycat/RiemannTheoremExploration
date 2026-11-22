# 解读 24 — Greenberg-Wiles 本体与供给装配收口

> 对应第二十四轮侦察。三件收口：TTT 定义体、GreenbergWilesAt 本体、supplyOfAdmOf 尾部闭合。

## 1. TwistedThetaTheorem 定义体（GL3Theta 943-950）

对每条曲线理想 cc（IsCurveIdeal）与每个判别式十二次根 δ：

per22(tor0 cc δ) ∧ (∃ chi, IsChi chi) ∧ 对每个特征 chi，存在 e: FamE 满足

vec22 ∧ th22(C) ∧ **eq22(tor0 cc delta, chi, e)** ∧ int22 ∧ mom22 ∧ LargerSupportMomentCondition ∧ str22 ∧ famItems ∧ X(cc, delta, e)

新细节：**eq22 把特征 chi 编进等式条件**——扭曲 Theta 的特征化版本（对每个特征有对应的矩等式）。九条矩 + famItems + X。

## 2. GreenbergWilesAt 本体（GalCoh.lean:175）——Euler 示性数平衡式

**前提**（即解读 04 的 PT 假设的基数版）：

- Sha1(rhoS) 与 Sha2(twDual muS rhoS) 均有限，且 **card Sha1 = card Sha2**（= Statement.lean 的 PTShaAt）
- 条件族：0 < r、l ≠ 2、ContainsAbove S l、连续作用、**muS 是分圆特征 mod l^r**（muS ∘ toGS = cycMod）、位提升、实位复共轭条件、局部条件 L（LocCond）

**结论（Greenberg-Wiles 平衡式）**：

card(Sel(rho, L)) × card(H0(twDual mu rho)) × (对 v in S 求积 card H0(rho|v)) × archH0Card
= card(Sel(twDual mu rho, L)) × ……（对偶侧平衡）

⇒ **这就是解读 04/08 "长度记账"的文献级原件**：带分圆扭转与局部条件的 Selmer Euler 示性数平衡。链条闭合确认：Statement.lean 四条 PT 假设 ⇒ GreenbergWilesAt ⇒ Selmer 基数公式 ⇒（Kato 有限性）⇒ Sha 窗口数值。

## 3. supplyOfAdmOf 尾部闭合

- hQS：宿主 QS ≤ C0·R.n（预算）
- hA 应用：通用供给产出宿主 H/q0（HostGood 十四条）
- **hprime：l | H.QS ⇒ l | 2·psi.N**（宿主 QS 的素因子全在 2·psi.N 内——QS 素因子限制）
- boundedTw：psi 的**有界扭转**（boundedTw.lean 角色落位）
- isChiField：psi + 宿主实例化 IsChiField（解读 03 判据在装配尾部落地）
- hv.mono：VVle 单调（与 noExc_mono 同款元模式）+ Scale.b/L 改写
- 输出 HostExW 四元组（R/H/q0/...）——**装配完整闭合**

## 4. 主干侦察完成宣告

24 轮侦察覆盖：收束链、经典桥、组装层、宿主舞台、Poitou-Tate、平方根截断、Landau 判据、放大机制、均方界、高度消失、TW/Kato 模性提升、GL3Theta/Kudla、GL4 分支链接、ζ 通道、Gz/Gm/判据桥——**主干已无未知区块**。剩余边角（LinkGLOBAL7 层级表细节、GL3Theta↔GL4 梯子、GL3Theta 前中部 900 行的 p-adic 细节）均为技术性深化，不影响架构理解。

## 下一步（侦察转向）

- [ ] **新数学结构与工具提炼报告**（用户核心要求：从 24 轮积累中正式提炼 UpperTheory 窗口体系/LiteralAutomorphy/宿主舞台/链绑定网络/形式桥架构等）
- [ ] 证明总览合成文档（全链一页式）
- [ ] 边角深化（按需）

