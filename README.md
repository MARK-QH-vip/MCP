# polaris-memory（ZCode 插件）

POLARIS 永久记忆 MCP —— 给 AI 编程助手装上长期记忆。

- **能力**：两级语义召回（值空间排序 + 反回声室混合读取）、空基线校准
  novelty 自动去重、GDPR 式定向遗忘、损坏存储自愈（隔离 + 文本重建）、
  跨进程共享存储零丢失。
- **商业模式**：个人用户免费，每月 **1000 次搜索额度**（自然月 1 日重置；
  写入/遗忘/统计/健康检查不消耗额度）。企业不限额度版本通过授权通道提供。
- **闭源发行**：`srv/polaris_mcp_closed.py` 为编译字节码捆绑件（v2.2.0），
  服务器源码不在本仓库分发。

## 安装

ZCode 客户端 → 插件市场 → 安装 `polaris-memory` 即可。MCP 服务以 stdio 方式
自动挂载（需要本机 Python 3.9+，torch + numpy）。记忆数据默认存于插件
`data/memory.pt`，可在 ZCode 设置 → MCP 中修改 `--storage`。

## 工具

`polaris_write` / `polaris_recall`（消耗额度） / `polaris_auto_remember` /
`polaris_novelty` / `polaris_forget` / `polaris_stats` / `polaris_health` /
`polaris_consolidate`

## 质量验证

- 28 项 pytest 全绿：工具语义、stdio/HTTP 协议、跨进程共享存储、配额引擎
- 16 项发布级硬化：千槽规模（召回 12ms）、5 轮硬杀零损坏、日志零隐私泄露、
  HTTP token/415/无 CORS、8 进程并发精确、损坏存储自愈
- 语义召回（BGE 白化）13 组查询值空间 top1 全对

## 反馈

问题与商务合作：通过 ZCode 插件页或本仓库 Issue 联系作者。
