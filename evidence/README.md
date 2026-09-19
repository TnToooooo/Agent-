# 运行证据（Run Evidence）

本目录收录**本人实跑**的原始证据文件，与 `task*.md` 的实验结果一一对应。Task 0 证据由教材配套脚本自动生成：`evidence.json` 记录运行配置、完整命令行、模型与端点、五臂结果、token 用量与判分；`evidence.sha256` 是同目录证据的自校验哈希。Task 1 证据为结果 JSON 与控制台输出文本（说明见各子目录 README）。

## 实验 1-1（context · 五臂消融）

| 目录 | 模型 | 时刻（UTC / 北京） | SHA-256 前 8 位 | 验收 | 对应本子 |
|---|---|---|---|---|---|
| `1-1/runs/real_20260916T130613Z` | MiniMax M3 | 13:06 / 21:06 | `22f10cb2` | `false` | ③ 运行档案第 1 行（主跑） |
| `1-1/runs/real_20260916T130757Z` | MiniMax M3 | 13:07 / 21:07 | `670eb4f9` | 单臂调试（no_tool_results） | 未入表 |
| `1-1/runs/real_20260916T130944Z` | MiniMax M3 | 13:09 / 21:09 | `e785e085` | 单臂调试（no_tool_calls） | 未入表 |
| `1-1/runs/real_20260916T133515Z` | MiniMax M3 | 13:35 / 21:35 | `574b2c47` | `false` | 未入表（复跑，用于比对波动） |
| `1-1/runs/real_20260916T133630Z` | GLM-5.3-Flash | 13:36 / 21:36 | `34a8a689` | `true` | ③ 运行档案第 2 行（主跑） |
| `1-1/runs/real_20260916T134857Z` | DeepSeek V4.1 Flash | 13:48 / 21:48 | `72acce7a` | `true` | ③ 运行档案第 3 行（主跑，断言全观察） |
| `1-1/runs/real_20260916T143331Z` | DeepSeek V4.1 Flash | 14:33 / 22:33 | `76257213` | `true` | ③ 运行档案第 4 行（复跑＝**现行 latest**） |
| `1-1/latest.json` | — | — | `76257213`（同上一行） | — | 脚本提升的现行验收证据 |

> 关键比对：21:48 与 22:33 两次 DeepSeek 运行**命令完全相同**，但 `no_reasoning` 臂分别为 `incorrect` 与 `correct`——该臂表现是 run-to-run 波动，非稳定属性（详见 `task0.md` ③ 的说明）。

## 实验 1-4（image-gen-workflow · workflow 路线）

| 路径 | 内容 |
|---|---|
| `1-4/runs/real_20260916T162657Z/` | 本次运行的 manifest（`evidence.json` + `evidence.sha256`）：5 需求 × 3 路线共 15 次执行记录、改写结果、图片 SHA-256、provider（改写 `zhipu` / 生图 `dashscope`）、用量 |
| `1-4/calls/*.json` | 16 份原始 API 调用留证（改写节点 4 份 + 生图节点 12 份，含请求与响应） |
| `1-4/images/*.png` | 4 张成图：`programmer-overtime`、`windowsill-plant`、`headphone-poster`、`future-city-morning` |

> 本轮 15 次执行中 4 次成图：workflow 路线 4/5（`agi-programmer` 败于改写节点输出非法 JSON）；`native`（0/5，SDK 未安装）与 `native_gptimage`（0/5，占位 Key 401）为预期内失败。

## 实验 2-10（context-compression · 六策略压缩对比，2026-09-19）

| 文件 | 跑次 | 模型 | 对应本子 |
|---|---|---|---|
| `2-10/experiment_20260919_155206.json` | 第 1 跑（补丁前） | deepseek-v4-flash | ③3.1 四跑汇总表 DS 首跑列 |
| `2-10/experiment_20260919_171222.json` | 第 2 跑（白名单补 deepseek） | deepseek-v4-flash | DS 重跑列 |
| `2-10/experiment_20260919_185046.json` | 第 3 跑（白名单补 glm，provider=zhipu） | glm-5.3-flash | GLM 跑列 |

> 作者基准（kimi-k3＋真 Serper）为教材数据，非本人实跑，不入本目录。本地补丁声明与扫描说明见 `2-10/README.md`。

## 实验 3-8（agentic-rag · Agentic vs 非智能体化 RAG，2026-09-19）

| 文件 | 内容 | 对应本子 |
|---|---|---|
| `3-8/compare_offline_console_20260919.txt` | ① 离线 7 题召回率：76%→100%（+24%） | ③3.2 ① 量化表 |
| `3-8/main_compare_console_20260919.txt` | ② 同题双模式完整答案（--no-verbose 重跑） | ③3.2 ② 质性表 |
| `3-8/first_run_truncated_log_utf8.txt` | 首跑截断日志副本（控制台缓冲截断，保留前 3 轮轨迹） | 过程记录 |

## 说明

- **收录范围**：本人 2026-09-16（Task 0：1-1、1-4）与 2026-09-19（Task 1：2-10、3-8）的实跑证据。实验 1-2（等效路径）未落证据文件（`main.py` 未加 `--output`），实验 1-3 尚未运行，故均不在本目录。
- **上游历史证据未收录**：`real_20260729…`、`real_20260825…`、`real_20260901…`、`probes_20260825T` 等为配套仓库自带的上游产物，不属于本人运行。
- **不含任何密钥**：所有证据均记录 `credential_value_recorded: false`，只保留环境变量名（如 `DEEPSEEK_API_KEY`、`MINIMAX_CN_API_KEY`、`ZHIPU_API_KEY`）。
- **校验方法**：`certutil -hashfile evidence.json SHA256`（Windows）或 `sha256sum evidence.json`（Linux/macOS），与同目录 `evidence.sha256` 的首段比对。
