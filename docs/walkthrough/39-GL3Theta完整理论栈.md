# 解读 39 — GL3Theta 完整理论栈：CM 形式群上的 Weil 相位理论

> 对应第三十九轮侦察。GL3Theta 107-199 行全解——这个 1013 行文件的完整理论栈定型。

## 1. 文件身份终定：CM 椭圆曲线形式群上的 Weil 相位理论

GL3Theta（1013 行）= 以下理论栈的完整形式化：

1. **形式群层**（68-107）：G1 图式 + Weierstrass p-adic 模型 + 形式对数 flog + ph/be/PhOn 相位函数 + hP 配对
2. **绑定层**（107-110）：At（曲线理想 + 判别式根 + 模型公理）
3. **Jacobi 分类层**（115-121）：SplitK（jacobiSym(−d,p) = 1，分裂）/ InertK（= −1，惰性）——**素数在 Q(√−d) 的分裂/惰性由 Jacobi 符号定义**
4. **模型存在层**（modelEx）：存在 IsModelU 模型；5 ≤ p ∧ InertK ⇒ ModelOverW（惰性位模型在 W 上）；‖C.u‖ = 1
5. **立方检验层**（cube2/cube3/cube）：ph 三次可加性
6. **双线性层**（beBiadd）：be 双加性
7. **积分层**（addInt/endInt）：运算保持积分性
8. **CM 规范层**（phNorm）：**phAt(mulBy α.1 Xv) ≃ (α.1·α.2)·phAt(Xv)**——CM 元素按**相对范数 N(α) = α.1·α.2** 缩放相位（CM 理论核心公式）
9. **共轭层**（beConj）：be(α.1 作用, X₁) ≃ be(X₀, α.2 作用)——**共轭对称**（α.1/α.2 互换）
10. **分裂消失层**（splitZero）：**SplitK p ⇒ be ≃ 0 ∧ ph ≃ 0**——分裂位上相位完全消失！
11. **对角层**（beDiag）：2·be(Xv, γ 作用 Xv) ≃ (γ.1+γ.2)·be(Xv,Xv)；**be(Xv,Xv) ≃ 2·ph(Xv)**——be 与 ph 的对角关系
12. **射流层**（jetPh/jetsPh）：i!·coeff_i 射流系数；p ≠ d ⇒ 整数；**p = d ⇒ ‖jetPh 2‖ ≤ √p**
13. **Taylor 化身层**（ser1/atU）：ser1(lam, G) = G 的各阶导数/n! 经 lam 的 p-adic 幂级数；**atU G = (C.u⁻¹·l) 代入 ser1(G)**——**代数函数 G 经形式对数坐标的 p-adic 级数化身**
14. **挠点层**（Tors1/transl/IsTwoTorsionPointUnkilled）：p-素数阶挠点；**挠平移下 ePhi1⁻¹·atU(U1(t)) 积分且常数项范数 = 1**；2-挠未杀伤判据（(1+i√d)/2 杀伤测试）
15. **Weil 算子层**（XiF/xiOne/xiMove/modelXi/movesCompose）：换格链 + 2-上循环（解读 34）
16. **族化层**（PhUnitary/PhIsotropic/PhDual/Adm3s/Statement 族）

## 2. 关键数学公式（原样转录）

- **CM 相对范数缩放**：phAt(mulBy α.1 Xv) ≃ (α.1·α.2)·phAt(Xv) —— N(α) = α.1·α.2（相对范数）缩放相位
- **分裂消失**：SplitK p ⇒ be ≃ 0 ∧ ph ≃ 0 —— 分裂位零化
- **对角关系**：be(Xv,Xv) ≃ 2·phAt(Xv) —— be 对角是 ph 的两倍
- **ser1**：G 的 Taylor 级数（iteratedDeriv n G 0 / n!）经 lam 的 p-adic 化身
- **atU**：形式对数 l 代入 ser1 —— **代数函数的 p-adic 级数化身**

## 3. 消失与分歧的二元结构

- **分裂位（SplitK，Jacobi = +1）**：be/ph 完全消失（splitZero）——「好位无贡献」
- **惰性位（InertK，Jacobi = −1）**：模型在 W 上（ModelOverW）且按 N(α) 规范化——「坏位有结构」
- **p = d（分歧位）**：jetPh 2 ≤ √p（临界收缩）

**素数三分类**（分裂/惰性/分歧）各自有独立的处理机制——这是解析数论的 classical 三分法在引擎中的完整体现（解读 18 三区定性的平行）。

## 4. U1 底层待溯

U1(Λ, t, sgStar)(z) 的定义在 GL3Theta 之外（imports：GeneralLinearActions.FiltrationBoundaryCriterion/FiltrationCocycleLiftCriterion/ParConsts）。从用法推断：U1 是与格 Λ、平移 t、特征 sgStar 相关的基本级数（疑似 Siegel 函数/Theta 常数类）。后续按需追溯。

## 下一步侦察队列

- [ ] U1 底层定义追溯（FiltrationBoundaryCriterion/CocycleLiftCriterion/ParConsts）
- [ ] GL3Theta 前段 60-107 行补遗
- [ ] LinkGLOBALPk FamGL 后续槽位

## 本轮结论

GL3Theta = **CM 形式群上的 Weil 相位理论完整栈**（16 层理论，1013 行）。它的数学密度是全证明之最——单文件包含：形式群、Weil 表示、CM 理论、Jacobi 分类、射流理论、挠点理论、换格链。「迷向消失」「分裂消失」「CM 相对范数缩放」「√p 临界收缩」四大机制在此同台。**读懂此文件 ≈ 读懂引擎的解析-几何接口的全部语义**。
