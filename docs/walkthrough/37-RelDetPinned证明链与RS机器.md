# 解读 37 — RelDetPinned 证明链与 Rankin-Selberg 球形机器

> 对应第三十七轮侦察。RelDetPinned 证明链完整 + Rankin-Selberg 球形机器定位。

## 1. RelDetPinned 证明链完整（RelDetAdelicOfPinned.lean）

- detId_eq：**detId = detFI(L')/detFI(L)（分式理想类）**——relDet 的类化还原
- pinned_of_equiv：**从乘法等价 e（兼容 e1DT 与 relDetT）构造 RelDetPinned**——钉住的构造路线
- **relDet_eq_of_pinned**（大定理）：CMData + dt 映射（unitaryOneFiniteAdeles → Dt，核=积分单位群）+ hUO + **hrat（GL₁ 行列式有理化）** ⇒ **D.relDet N L L' = dt(x) 的商群像**——adelic 相对判别式由单位群映射像给出
- 证明骨架使用 **powRatAll_of（解读 33 GL3Theta 的）+ NormOnePowerPrincipal（normOne_pow）+ detId_eq + coe_eq_of_pow + val_eq_pow**——跨文件复用实锤
- **pinned_of_finer**：SQ 素数集细化版——从 DtQ（SQ 变体）+ modEquiv 构造 RelDetPinned——**Pinned 非空的构造路线定谳**（解读 35 的 Pinned 谜底完整）

⇒ RelDetPinned 语义最终定位：**adelic 相对判别式（relDet）与类域映射（dt）的一致性钉住**——adeles + 类理想 + 分式理想类的类域论语言。

## 2. phW 同名现象修正

EtaleSheaves/RTEqZeroOfPtA.lean 的 phW（étale 场景）与 GL3Theta 的 StatementPhaseWitt 不同源——**同名异义再次出现**（AI 生成命名冲突）。PhaseWitt 的真身待 GL3Theta 内部查找。

## 3. Rankin-Selberg 球形机器（AutomorphicSpectrum/BlockDecomposition/NormCpowLtOne）

unramified_sum 定理（超长陈述）的组件：

- **Spherical.sphericalWhittaker**——球形 Whittaker 函数（GL(n) 自守表示的规范向量 Whittaker）
- **Spherical.schur ![a, b, 0]**——**Schur 多项式**（GL3 的对称群表示多项式——Satake 参数的代数包装）
- **Rankin-Selberg 卷积 L 因子**：∏_{i∈Fin 3, j∈Fin 2} (1 − λ_i · y_j · q^(−s))⁻¹ —— **GL3 × GL2 的 RS 卷积局部因子**
- GL2LocalData.dW3/dW2 —— GL2 局部数据

**定性**：BlockDecomposition 区含 **Rankin-Selberg 卷积 + 球形 Whittaker + Schur 多项式**——GL3 × GL2 的自守 L 函数局部理论（经典 Jacquet–Piatetski-Shapiro/Jacquet-Shalika 机器）。

## 4. 常数谜语收官状态

401/400/52/3-2/15/7/eD/eL/1728/8/2-3 翻转/C22/C3/CrystallineComparison——**全部已定谳或有明确归属**。仅剩 C22 的数值语义（十二次根特征 Theta 族常数）为最小遗留。

## 下一步侦察队列（低优先）

- [ ] C22 数值语义
- [ ] GL3Theta 521-700 与 780-941 行的残留段
- [ ] UPDATE.md 全面整理（25+ 轮积累）

