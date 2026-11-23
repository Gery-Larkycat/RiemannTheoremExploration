# 数学背景 36 — Witt 向量浅尝：p-adic 世界的另一种坐标

> 面向零基础读者。读完你将对源码中的 PhaseWitt（Witt 相位）有一个基本的心智图。本文只做浅层介绍——Witt 理论本身极深。

## 1. 为什么需要 Witt 向量

p-adic 整数 Z_p 是个环，但"特征 p 的世界"（F_p 及其扩张）与它之间的桥梁并不平凡。**Witt 向量** W(F_p) ≅ Z_p：给特征 p 的域配上一种特殊的多组分量的"环结构"，恰好还原 Z_p。

- Witt 向量是一组坐标 (w₀, w₁, w₂, …)，加法/乘法用"幽灵多项式"定义（ghost components）
- p-typical Witt 向量是 p-adic Hodge 理论（解读 16 的 Bhatt-Scholze 晶体/棱柱）的基本语言

## 2. 本引擎的 PhaseWitt

GL3Theta 尾部声明 StatementPhaseWitt := phW D——**相位函数的 Witt 版**。推测语义（浅层）：Weil 相位函数 wPh 在 Witt 坐标下的表达——相位信息从 (−1)^m 型符号升级为 Witt 分量结构。深语义待验证。

## 3. 与其他笔记的连接

- 笔记 21（p-adic 世界）：Z_p/Witt 的关系 = 坐标系与精化坐标
- 笔记 16（Deligne/Kato）：晶体上同调的语言就是 Witt/棱柱语言
- 解读 34（2-上循环）：Witt 结构可吸收部分上循环信息

## 术语速查

| 术语 | 一句话 |
|---|---|
| Witt 向量 | 特征 p 世界到 Z_p 的特殊坐标 |
| ghost 分量 | Witt 加乘的幽灵多项式 |
| p-typical | 以 p 为基的 Witt 标准形 |

## 与源码的对照

| 源码 | 本篇概念 |
|---|---|
| StatementPhaseWitt / phW | 相位的 Witt 结构 |
| JetTorsionCompatibility | Jet（射流）挠相容 |
| ThetaDivisorCompatibility | Theta 除子相容 |
