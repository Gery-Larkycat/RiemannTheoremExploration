# 解读 23 — TwistedThetaTheorem 陈述解剖与 Weyl 维数容许界

> 对应第二十三轮侦察。GL3Theta 主定理形态定型；AdmittedWeylDimension 定性。

## 1. TwistedThetaTheorem 陈述解剖（GL3Theta 928-953 行）

核心定义三件：

- **aux₃ D**：对数量规的分解 = LatticeGrowthBound（格增长界）∧ SplitModelProperties（分裂模型性质）∧ DeterminantCharacterProperties（判别式特征性质）∧ readW（读数 W）
- **Adm3s D**：容许三件 = admJ（J 容许）∧ **InducedCMType**（诱导 CM 型）∧ HostFieldConditions（宿主域条件）
- **Stmt D := Adm3s D → aux₃ D** —— GL3Theta 主定理形态：容许性 ⇒ 对数量规

**TwistedThetaTheorem (D) (C) (X)**：X 是"额外断言"谓词（Ideal → C → FamE → Prop），C 是结论常数；**ConclusionE (D) (C) := TwistedThetaTheorem D C (fun _ _ _ => True)**（X 取恒真）。.mono：X 蕴含 X' 时定理传递。.rec（解读 22）在补丁条件下产出九条矩条件。

⇒ **语义**：TwistedThetaTheorem 是"扭曲 Theta 的模性主定理"的参数化形式（C = 结论强度，X = 附加要求）——模性结论以**常数可调**的方式供给下游（下游可以按需要求多强的 X）。KudlaFamilyStatement 等是它的特化族。

## 2. InducedCMType：CM 型的诱导（Adm3s 成员）

解读 17 的 Kstar = Q(√−q) 是 CM 域（带复乘型：共轭嵌入的对偶对）。**InducedCMType** 表示该 CM 型被"诱导"到引擎的更高层级结构（D7 数据）上——虚二次域的 CM 型是构造整个宿主/层级/窗口体系的**初始对称性数据**。

## 3. AdmittedWeylDimension（151 行，GlobalSchurBounds）

- 基座：**GAf D**（adelic 仿射群——G_Af，GlueSmooth/Iwasawa 分解中的群）、LevelData 层级数据、Word/ColRep 列表示
- TrivStab / LevelDataRankBound / BaseWeightColumnCondition —— 稳定子平凡、秩界、基础权重列条件
- **AdmittedWeylDimension D**（56 行）：容许 Weyl 维数命题

**语义**：GL3Columns（解读 11）列表示的**Weyl 维数公式**（不可约表示维数 = Weyl 公式）被容许界控制——表示维数是"列格"的大小参数，其界进入链绑定的尺寸账本（ChainTied 的 m f Top 等）。

## 4. 悬而未决（收尾清单更新）

- TwistedThetaTheorem 定义体 943-950 行内部（X 的精确调用方式）
- GL3Theta ↔ GL4 梯子
- supplyOfAdmOf 尾部（100 行后）
- LinkGLOBAL7 层级表

## 下一步侦察队列

- [ ] TwistedThetaTheorem 943-950 行定义体
- [ ] supplyOfAdmOf 尾部收口
- [ ] GreenbergWilesAt 定义体（GalCoh.lean:175）

