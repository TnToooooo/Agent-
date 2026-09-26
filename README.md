# 深入理解 AI Agent · 共学笔记

> **教材**：《深入理解 AI Agent：设计原理与工程实践》v2.0（2026-09-06），李博杰 著
> **教材配套实验仓库**：[bojieli/ai-agent-book](https://github.com/bojieli/ai-agent-book) —— 本笔记所有实验均出自该仓库（实验代码 MIT 许可，版权归作者）
> **本仓库只收录个人学习笔记与本人实跑证据**——不含教材原文、不含 PDF、不含任何密钥。

## 我的学习环境

| 项 | 值 |
|---|---|
| Agent 运行时（harness） | **DeepSeek Harness（DSH）`0.1.5-rc.2`** |
| 驱动本会话的模型 | **DeepSeek V4.1 Flash**（DSH 侧调用 id：`deepseek-flash`） |
| 实验调用的模型 | **DeepSeek V4.1 Flash**（教材侧注册表 id：`deepseek-v4-flash`） |

## 学习计划

- **周期**：2026-09-17 → 2026-10-06，共 20 天，每天约 5 小时（2026-09-26 通知：自 Task 2 起各截止顺延一天）
- **共 7 个 Task**，每 3 天一个，**硬截止**（逾期报离群）

| Task | 主题 | 截止 | 对应章节 | 笔记 |
|:--:|---|---|---|---|
| 0 | Agent 基础与环境准备 | 09-17 03:00 | 第 1 章 AI Agent 入门 | [task0.md](task0.md) |
| 1 | 上下文工程与 Memory / RAG | 09-20 03:00 | 第 2–3 章 | [task1.md](task1.md) |
| 2 | Tools 与 MCP | 09-24 03:00 | 第 4 章 工具 | [task2.md](task2.md) |
| 3 | Coding Agent 与 Agent 交互 | 09-27 03:00 | 第 5–6 章 | [task3.md](task3.md) |
| 4 | Agent Evaluation 与模型能力优化 | 09-30 03:00 | 第 7–8 章 | [task4.md](task4.md) |
| 5 | Agent 持续进化与 Multi-Agent | 10-03 03:00 | 第 9–10 章 | [task5.md](task5.md) |
| 6 | 共学总结 | 10-06 03:00 | 全书回顾 | [task6.md](task6.md) |

> 页码口径：笔记中的 `p.N` 为 **PDF 物理页**；书内印刷页码 = PDF 页码 − 8。

## 笔记结构

每个 Task 独立成文，固定六段：

| 段落 | 撰写人 |
|---|---|
| ① Task 概述 | agent |
| ② 实验过程 | agent 写步骤 → 本人跑的过程中补充 |
| ③ 实验结果 | 本人 |
| ④ 我的理解 | 本人 |
| ⑤ 思考题 | agent 出题 → 本人作答 → agent 点评 |
| ⑥ 本章重点概念及描述 | agent |

## 思考题点评的四条准则

1. **辩证思维**——不走极端，看两面与适用条件
2. **实践出真知**——能用实验 / 数据说话就不空谈
3. **具体问题具体分析**——拒绝套话与万能答案
4. **采纳互联网最新的可信事实**——时效性信息现查现证

## 运行证据

[`evidence/`](evidence/README.md) 收录本人实跑实验的原始证据（脚本自动生成，非手写）：

| 实验 | 证据 | 要点 |
|---|---|---|
| 1-1 五臂消融 | `evidence/1-1/runs/`（7 次运行）＋ `latest.json` | 每份含完整命令行、模型端点、五臂结果、token 用量与判分；附 `evidence.sha256` 自校验哈希 |
| 1-4 工作流生图 | `evidence/1-4/` | manifest ＋ 16 份原始 API 调用留证 ＋ 4 张成图 |

证据内**不含密钥**（只记录环境变量名）；校验方式见 [`evidence/README.md`](evidence/README.md)。

## 声明

- 笔记中的引用均标注页码出处，仅用于个人学习与研究；**不收录教材原文全文**。
- 仓库采用**白名单式 `.gitignore`**：默认排除一切，只放行 `README.md`、`task*.md` 与 `evidence/`。教材 PDF、全书文本、API 密钥、实验代码克隆均被挡在版本控制之外。
