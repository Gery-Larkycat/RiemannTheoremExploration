# 更新记录

## 2026-11-23

- 项目创建：目标为 clone Alpöge–Claude 黎曼定理 Lean 证明并合作解析阅读（README.md）
- 新闻调研：确认 2026-11-20 证明发布、Lean/Mathlib 社区认证、Riemann@home 分布式验证等事实，沉淀至 README
- 术语决策：统一称「黎曼定理」（docs/DECISIONS.md D1）
- 方案决策：只读不编译（D2）、源码放 Linux 工作目录（D3）、手动分片下载（D4）
- 启动官方档案下载：14 分片并行，239 MB，下载后 sha256 校验解压
- 下载完成：分片字节合计与官方一致，sha256 校验 OK，解压 175,190 文件 / 17,374,215 行
- 结构预览：顶层 11 个 lean_lib 模块（GroundTheory / CompanionTheory / Development / Lemmata 等）；入口 Main.lean 仅 12 行、Statements.lean 仅 16 行，最终归结自 Supplements.Kernels.MainTheoremsAll 的 rhOfAll
- 主线收束链闭合（docs/PROOF-MAP.md）：EveryCharacter（引擎）→ Formalism.VW 桥（GammaFactorNonvanishing/CritLine，32 行）→ RH；结构 = Hadamard–de la Vallée Poussin 反射法复活，新数学在引擎侧 GlobalTheory.GLq.Green + UpperTheory.Top
- 数学背景笔记启动：docs/vibe-coding/knowledge4newbee/riemann-proof/01-函数方程反射法.md
- 项目定位升级（用户指令）：大量补充数学背景 + 重点提炼新数学结构与新工具；增加证明过程解读文档化（按侦察顺序成文，docs/walkthrough/）
- 第二轮侦察：GlobalTheory.Published 文献库清单、WeilBound 分析机器结构、TopPlug 19 行组装点、EveryCharacterE 配料清单；新概念嫌疑 LiteralAutomorphy / BoundAtTwoAndThree / CovolX
- 文档产出：docs/walkthrough/01、02，数学背景笔记 02-Theta对应与SiegelWeil，PROOF-MAP 引擎侧增补
