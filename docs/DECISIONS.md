# 决策记录

## D1 — 术语统一：称「黎曼定理」
- **背景**：2026-11-20 Alpöge–Claude 证明发布并经验证，猜想已成定理。
- **决策**（用户拍板）：本项目文档与交流一律称「黎曼定理」；涉及历史脉络时注明原称「黎曼猜想」。
- **备选**：沿用「黎曼猜想」——被否，与已证明的事实不符。

## D2 — 只读不编译
- **背景**：完整编译 lake build Main 需约 160 GB 工作空间、快机约 2 天；Riemann@home 已有全球多人独立编译验证通过（编译结果一致、仅依赖三标准公理）。
- **决策**（用户确认）：不做本地编译验证，项目聚焦解析、理解、阅读。
- **备选**：本地完整编译以亲测验证——被否，增量价值低、成本高；未来如有需要可再议（阶段 2 预留）。

## D3 — 存放位置：Linux 工作目录
- **背景**：用户提 Windows 系统盘 400GB；实测 NTFS 盘挂载于 /media/larkycat/Windows 且为只读（Windows 快速启动/休眠所致），且 FUSE 挂载对海量小文件 IO 慢。
- **决策**：档案与源码放当前 Linux 工作目录（根分区余 174GB，阅读仅需约 2.5GB），Windows 盘暂不启用。
- **备选**：解决只读挂载后放 Windows 盘——被否，无必要；若未来阶段 2 编译落地再评估。

## D4 — 下载方式：手动分片下载 + 校验
- **背景**：riemann-at-home 官方 CLI 会装到固定目录（Linux 为 /opt/riemann-at-home）并含注册/上传流程，与本项目「只读」定位不符。
- **决策**：手动按官方元数据下载 14 分片（curl 并行）→ 按序拼接 → sha256 校验 → 解压。元数据（分片数、总字节、sha256、工具链、Mathlib rev）取自官方 CLI 源码常量。
- **备选**：直接运行 riemann-at-home CLI——被否，安装位置与副行为不受控。

## D6 — 项目改名 RiemannTheoremExploration
- **背景**：用户在 README 已将标题改为「RiemannTheoremExploration — 黎曼定理 Lean 证明业余探索」，remote 仓库名同名，并指示本地目录同步改名。
- **决策**：本地目录 mv 为 RiemannTheoremExploration；文档中项目名随改，简称不变（「黎曼定理」称谓不受影响，见 D1）。

## D7 — MIT 协议
- **背景**：用户指定开源协议。
- **决策**：LICENSE 采用 MIT，版权行 Copyright (c) 2026 Larkycat (Gery-Larkycat)。

## D8 — 每次提交后自动同步 remote
- **背景**：用户要求每次 commit 后自动 push；remote 已配置 origin=https://github.com/Gery-Larkycat/RiemannTheoremExploration.git。
- **决策**：执行纪律约定——每次 commit 后立即 push origin main（当前分支 main）；推送失败时记录原因并继续本地工作，不阻塞阅读主线。未使用 post-commit hook（避免 hook 内网络失败阻塞提交）。

## D5 — git 用户配置占位
- **背景**：本机无全局 git user.name/email，commit 需要身份。
- **决策**：仓库级配置 user.name=larkycat、user.email=larkycat@localhost（本地占位，仓库无远端推送需求）。

## D9 — 两项执行待办（改名与推送认证）

- **本地目录改名待办**：父目录 /home/larkycat/source/playground 为只读挂载（DSH 提权后仍报 Read-only file system），目录级 mv 无法自动执行。项目名已在 README/remote/文档层生效，本地目录名暂维持 RiemannTheorem。**待办**：用户在自己的终端执行
  mv /home/larkycat/source/playground/RiemannTheorem /home/larkycat/source/playground/RiemannTheoremExploration
  之后会话工作目录随新路径迁移（关联 D6）。
- **远端自动推送待办**：本机无 GitHub 凭据（无 SSH key、gh 未登录、无 credential store），HTTPS push 报 could not read Username。自动推送暂不可执行（关联 D8）。**待办**：用户提供任一认证（gh auth login / SSH key / PAT 配 credential store）后恢复每 commit 即 push；此前本地提交排队，用户亦可随时自行 push。

