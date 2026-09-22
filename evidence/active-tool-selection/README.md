# active-tool-selection 实跑证据（2026-09-22；agent 代跑，经用户授权）

| 文件 | 内容 | 对应本子 |
|---|---|---|
| `ats-results-20260922.md` | ① offline（35→400 scaling 全表）、② compare（qwen-plus 三策略表＋qwen3.7-plus 首跑留档）、③ compare 400（离线＋在线 qwen-turbo 三策略表）——原始输出直出控制台，本文件为逐表转录版 | task2.md ③ 主跑二全部表 |
| `03-compare-400-receipt.txt` | ③ 首跑收据：离线 400 段完整数据＋在线段 403 原始报错＋逐模型额度探针记录＋额度战役终局台账 | ③ 的过程存档 |

- 空文件 `01-offline.txt`／`02-compare.txt`（早期重定向失效产物）未收录。
- **不含任何密钥**：收据与转录仅含报错文案、模型名与统计数字；凭证模式扫描命中 0。
- 校验：`SHA256SUMS.txt`（`certutil -hashfile <文件> SHA256` 或 `sha256sum <文件>` 比对首段）。
