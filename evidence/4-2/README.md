# 4-2 perception-tools 实跑证据（2026-09-22；agent 代跑，经用户授权）

| 文件 | 内容 | 对应本子 |
|---|---|---|
| `01-smoke.txt` | MCP 冒烟：sdk=2.2.0、protocol=2026-07-28、tools=127、file_reader 真调 | task2.md ③ 表第 1 行 |
| `02-list.txt` | CLI 工具清单（54 个原生直调，按五类分组） | ③ 表第 2 行 |
| `03-demo-offline.txt` | 离线 5 步演示（grep/知识库命中、联网步跳过、私有数据结构化失败） | ③ 表第 3 行 |
| `04a-grep.txt` … `04i-document_reader.txt` | ④ 九个免 key 工具逐个真调（含 `04e`/`04g` 两个网络阻断失败记录，如实保留） | ③ 表 ④ 各行 |
| `05-image_analyze.txt` | qwen-vl-max 视觉分析（国内站；usage 660 tok、latency 5.846s、response_id 回执） | ③ 表 ⑤ 行 |
| `2-4B-min-agent.txt` | 2.4 B 档最小 MCP 客户端 agent 全过程：2 轮判断、3 tool_calls、0 错误、中文终答 | ③ 末节"2.4 B 档" |
| `SUMMARY.txt` | 13 步批量驱动的逐步骤 exit/耗时/行数汇总 | ③ 表总览 |

- 驱动脚本 `run_all_20260922.ps1` 与 B 档源码 `min_mcp_agent.py` 留于本地 `ai-agent-book/`（按发布约定不入库）。
- **不含任何密钥**：全部日志无 key 值（key 仅存本地 `.env`，不入库、不入日志）；凭证模式扫描命中 0。
- 校验：`SHA256SUMS.txt`（`certutil -hashfile <文件> SHA256` 或 `sha256sum <文件>` 比对首段）。
