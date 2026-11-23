# 解读 36 — RelDetPinned 生态与 GL3Theta 二十接口族（轻量轮）

> 对应第三十六轮侦察（轻量轮）。

## 1. RelDetPinned 生态

- 定义处：AbelianVarietyTheory/Definitions/Foundations/LatticeIntegralCoordinates.lean:271（**Pinned D := 存在 idl, RelDetPinned D idl**）
- 证明处：Proofs/IwasawaDecomposition/RelDetAdelicOfPinned.lean:564（**relDet_eq_of_pinned**——adelic 相对判别式的 pinned 版公式）
- 下游使用：JetTorsionCompatibility（Jet 挠相容）、ThetaDivisorCompatibility（**Theta 除子相容**——Theta 理论与除子理论的接口）、chiRec_bot（chiRec 在零格 = 0）

## 2. GL3Theta 内部二十接口族全录（835-941 行）

GL3Theta 后段定义了 20 个 Statement 接口（GL3Theta 内部的小形式桥）：

- **模型系**：StatementModelExists（admJ ⇒ modelEx）/ ModelShort
- **积分系**：StatementAdditiveIntegral / StatementEndomorphismIntegral
- **立方系**：StatementCubeSecond / CubeThird / Cube
- **双线性系**：StatementBilinearAdditive / BilinearConjugate（be 共轭）/ BilinearDiagonal（be 对角）
- **相位系**：StatementPhaseNorm / JetsPhase（Jet 相位）/ **PhaseUnitary（相位酉）** / **PhaseIsotropic（相位迷向）** / **PhaseDual（相位对偶）** / **StatementPhaseWitt（相位 Witt！）**
- **特殊情形**：StatementSplitZero（分裂零）/ **StatementAtTwo（在 2 处）** / StatementTranslation（平移）
- **正交存在**：StatementOrthonormalExists（InducedCMType + HostFieldConditions ⇒ orthoEx 标准正交存在）

**组织学**：GL3Theta 单文件 1013 行内含"形式群公理 → Weil 相位 → Witt 结构"的完整理论栈 + 自带接口族——AI 生成的"理论密度"惊人（单文件独立成理论单元）。

## 3. 新词汇登记

beConj / beDiag / splitZero / atTwo / transl / jetsPh / PhUnitary / PhIsotropic / PhDual / orthoEx / **phW（Witt 相位）** / JetTorsionCompatibility / ThetaDivisorCompatibility / chiRec

## 下一步侦察队列（按需）

- [ ] relDet_eq_of_pinned 公式本体（564 行）
- [ ] PhaseWitt / phW 的定义（Witt 理论层）
- [ ] GL3Theta 前中部 900 行 p-adic 细节

