# 数学背景 43 — Theta 提升构造 Galois 表示：权一实现

> 面向零基础读者。读完你将理解「从 Theta 级数造出 Galois 表示」这一现代数论的标志性行为，以及它与解读 16 Deligne 表示的分工。

## 1. 两种造表示的方式

- **Deligne 方式**（解读 16）：从模形式（尖形式）的 Hecke 特征值构造二维表示——输入是模形式
- **Theta 提升方式**（本引擎 galoisRepresentations_of_thetaLift）：从 Theta 级数与检验函数的积分理论构造表示——输入是 Theta 机器

权一（weight one）情形（Hodge-Tate 权 1）：对应「解析延拓最微妙」的一类表示—— holomorphic Lefschetz 公式 + Kodaira-Spencer 组装（rosetta Rank 4/6）。

## 2. Row0b recT：行 0b 递归参数

「行」（Row）是引擎的离散编码词汇（解读 26 的行/列/字母）：Row0b = 第 0b 行结构，recT = 递归参数（recursion parameter）。

**语义**：Galois 表示的局部-全局相容性以「递归参数」形式供给——每层递归使用上一层参数。这与 TW patching（解读 15）的递归补丁结构呼应。

## 3. 汇合点意义

引擎有两条供给腿：

- 解析腿：Theta/Siegel-Weil → 窗口（VWin）
- Gal 腿：Kato Theta 提升 → 权一表示 → Row0b

**RowSrc 是两腿的汇合螺栓**：Gal 参数进入宿主装配，与解析窗口共同触发 EveryCharacter。

## 术语速查

| 术语 | 一句话 |
|---|---|
| Theta 提升 | Theta 积分构造的自守表示迁移 |
| 权一实现 | Hodge-Tate 权 1 的几何实现 |
| Row0b | 行 0b 递归参数（离散编码）|
| 命名空间载体 | namespace 层级的物理文件 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| RowSrc.lean（8 行）| 命名空间载体枢纽 |
| galoisRepresentations_of_thetaLift | Theta 提升 → 表示 |
| tLiftK | Kato 侧 Theta 提升 |
| Row0b recT | 局部-全局递归参数 |
