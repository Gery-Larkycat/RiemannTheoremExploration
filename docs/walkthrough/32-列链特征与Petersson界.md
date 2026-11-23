# 解读 32 — 列链特征体系、类群特征和与 Petersson 界

> 对应第三十二轮侦察。GL3Theta 中段（460-520 行）与 LocalQuadraticParts（807 行）两大金矿。

## 1. rhoCh 列链特征体系（GL3Theta 460-520）

- rhoOf/rhoOf'：列 i 的特征 = 列特征 mt(i+1) 与 **CM 特征 chiD 的半幂扭转**（chiD^(−N(i+1)/2) / chiD^(N(i)/2)）——**层级宽度的一半进入扭转指数**
- CarriesTupleCharacters：**列链携带元组特征**（rhoDet 读数 = rhoCh 特征取值）
- rhoThreeOf 三性质：有理幂取值 Mod1E（代数整数单位）、UO 元素有限阶、**e1Dt z 的嵌入公式** rhoOf(e1Dt z) = Π_tau embT(z)^(−sSharp(i,tau))——**斜率族 sSharp 的嵌入级实现**（解读 30 斜率族的运行层）
- **lift_eqC（类群特征和公式）**：C.K i phi c' = Σ_c (1/card(stab i c))·(rhoOf·rhoOf')•divDe i(...)——**稳定子倒数加权 × rho 特征乘积 × 除子元素**的求和

⇒ **解读 22 "类群特征和"的显式实现**：K 级数 = 类群特征加权的除子级数——宿主读数窗口的数值由此而来。

## 2. LocalQuadraticParts：局部二次部分 + Petersson 界（807 行）

- Loc 结构（局部数据）、nTT（宿主测试点数）、iotaQ/Z0（线性映射与子模块）、adm1（容许）
- **PeterssonBoundAtEmbedding / AllEmbeddings / FixedEmbedding** —— **Petersson 界**：自守形式的 L² 内积公式（AmbForm 周围形式在嵌入 s 处的界）
- DivisibilityLatticeMetricCondition / RRMetricDef / QPart —— 整除性格度量条件与 Q 部分

**定性**：LocalQuadraticParts = **均方界（解读 18）的引擎室**——Petersson 公式是特征和均方估计的文献级标准工具（L² 内积展开为特征和），"局部二次部分"即 L² 展开中的二次项。

## 3. 主链补全（第 32 轮后）

类群特征和（rhoCh + lift_eqC，本轮）→ 宿主读数窗口 → Poitou-Tate 记账 → … → RH。同时 Petersson 界（本轮）与均方区（解读 18）连接——均方估计的"文献级工具箱"（Petersson）与"引擎级装配"（MeanSquareBounds/pairEx）对接。

## 下一步侦察队列（持续边角）

- [ ] Petersson 界的引用链（谁消费 PeterssonBoundAllEmbeddings）
- [ ] rhoThree 的供给链（sSharp 嵌入公式的证明）
- [ ] GL3Theta 521-960 行（Theta 构造与 TwistedThetaTheorem 证明本体）

