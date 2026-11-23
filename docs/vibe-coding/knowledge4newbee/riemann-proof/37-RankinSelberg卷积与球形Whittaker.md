# 数学背景 37 — Rankin-Selberg 卷积与球形 Whittaker

> 面向零基础读者。读完你将理解"两个 L 函数相乘"的标准理论（Rankin-Selberg），以及球形 Whittaker 函数的角色。

## 1. Whittaker 函数：自守形式的"傅里叶系数"

自守形式沿 Whittaker 模型（对加法特征做傅里叶展开）的分量。**球形 Whittaker 函数**（spherical Whittaker）：在紧子群不变的规范向量处的 Whittaker 函数——它在每个素数位有**显式局部因子**。

## 2. Rankin-Selberg 卷积：两个 L 函数的乘法

GL(n) 表示 π 与 GL(m) 表示 π' 的 **Rankin-Selberg 卷积 L 函数**：

L(s, π × π') = 对素数 p：∏_i ∏_j (1 − α_i(π)·α_j(π')·p^(−s))^(−1)

（α 是 Satake 参数——解读 15。）

**局部因子**是标准欧拉因子（本引擎 NormCpowLtOne 的 ∏(1 − λ_i y_j q^(−s))⁻¹ 正是 GL3×GL2 版本）。**Schur 多项式**（对称群表示论）包装 Satake 参数的组合——GL3 情形 Schur ![a,b,0]。

## 3. 为什么要卷积

- 卷积 L 函数控制**两个算术对象的联合分布**
- 均方估计（解读 18）、逆向定理（解读 18 的 Converse Theorem）、特殊值（解读 16）全都使用 RS 卷积
- **本引擎语境**：GL3×GL2 卷积 = Theta 侧（GL3？）与 Dirichlet/L 侧（GL2）的联姻——波的联合控制

## 4. normCpowLtOne 的语义

文件名直译：**范数 C 幂小于 1**——某范数的 C 次幂 < 1（收敛因子）。与局部因子 ∏(1 − λy q^(−s))⁻¹ 结合：当 λy 项被压小时局部因子接近 1——**L 因子被"驯服"**。这就是均方/窗口界能传导到 L 函数的机制之一。

## 术语速查

| 术语 | 一句话 |
|---|---|
| Whittaker 函数 | 自守形式的傅里叶系数载体 |
| 球形向量 | 紧群不变的规范向量 |
| Rankin-Selberg 卷积 | 两个 L 函数的乘法理论 |
| Schur 多项式 | Satake 参数的对称群包装 |
| 局部因子 | 欧拉乘积的单素数因子 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| Spherical.sphericalWhittaker | 球形 Whittaker 函数 |
| Spherical.schur ![a,b,0] | GL3 Schur 多项式 |
| ∏(1 − λ_i y_j q^(−s))⁻¹ | RS 卷积局部因子 |
| NormCpowLtOne.lean | 范数幂收敛驯服 |
| GL2LocalData.dW3/dW2 | GL2 局部数据 |
