# 解读 33 — LiftObj 提升对象与 IsKer：进入证明本体深层

> 对应第三十三轮侦察。GL3Theta 521-600 行——声明层之下第一个构造性证明层。

## 1. lift_eq 全局确认

lift_eqC（解读 32）的全局版：列链 K 量 = Σ (1/card(stab)) · (rhoCh · rhoCh') • divDe——**类群特征加权的除子级数**在全部 Word u 上成立。

## 2. 多项式工具组（applyAt0/FrV/evFr/polD）

- applyAt0：从多元多项式 P 提取 **Taylor 系数组合**（Σ coeff·Π factorial·taylor 项）
- FrV：索引类型 = Tau × Fin N × Fin N（帧坐标）
- evFr：多项式在帧矩阵处的求值
- polD：多项式的**降维代入**（从 N 级到 N' 级的投影——s 加权三角代入）

## 3. IsKer：Theta 的代数系数有限组合谓词（核心！）

IsKer D T e S L L' Θ：

存在有限和表示 **Θ = Σ_k r_k · U(T, t_k, e)(z)**，其中：

- **系数 r_k ∈ Q̄**（代数数！）
- **p-adic 积分性**：p ∉ S 时 ‖lam(r_k)‖ ≤ 1（S 外全部单位）
- t_k 有公共整除指数 a（素因子全在 S 中）
- S 是特殊素数集（解读 26 BoundAtTwoAndThree 的 S = {2,3} 呼应——**特殊素数集 S 终于现形**）

⇒ **IsKer = "Theta 函数是代数系数有限组合"的谓词**——Kudla 理论的代数性核心（Theta 值不仅存在，而且是代数的、积分的、结构化的）。

## 4. LiftObj 提升对象规范（巨型结构体）

mt 列特征 / SDLat 格（Hida 式 SD 格）/ lattice_integral_coordinates（格积分坐标）/ dt 类映射（dt_lat：商群 = relDet 相对判别式）/ **c13**（CarriesTupleCharacters——解读 32）/ frm 帧矩阵系（**frm_inj 注入、frm_range 满射=行列式非零、frm_de de=行列式**——帧的完备规范）/ **dgen 生成元**（在中间数域 M 中主化：ellT = Z_M·s——**数域中间域 M 的主化**，解读 26 NormOnePowerPrincipal 的数域版）/ S 素数集 / Th Theta 函数族

## 5. liftTie：提升绑定

(∀ c c', IsKer 于相邻格对) ∧ 多项式相容（unf∘evFr = applyAt0∘polD∘Th）——**格对之间的 Theta 有限组合性 + 多项式相容性**。

## 6. 本轮结论

GL3Theta 的证明本体构造 **LiftObj（提升对象：列特征+格+帧+生成元全规范）** 并证 **liftTie（IsKer + 多项式相容）**——把"Theta 导数模性"实现为"**Theta 函数的代数系数有限组合的显式构造**"。这是全证明中最深的技术层之一（解读 22 的 Kudla 理论落地处）。

## 下一步侦察队列（持续边角）

- [ ] TwistedThetaTheorem 主定理的证明体（rec 组合器的输入从何构造）
- [ ] Petersson 界引用链下游（PointPropertyEqSizeFree / FreeFamilyOfLeaves）
- [ ] U(T, t, e)(z) 的定义（IsKer 中的基础函数）

