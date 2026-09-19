# 实验 3-8 运行证据（Agentic vs 非智能体化 RAG）

## 收录范围

本人 2026-09-19 晚实跑的控制台输出（UTF-8 文本）。`main.py` 的 compare 模式只打印不落盘，故以控制台全文为准：

| 文件 | 内容 |
|---|---|
| `compare_offline_console_20260919.txt` | ① `compare_offline.py`（零 API）：7 题证据召回率对照，单次 76% → 分解 100%，检索次数 1.0→1.3 |
| `main_compare_console_20260919.txt` | ② `main.py --mode compare --no-verbose`（deepseek-v4-flash＋离线 BM25）：同题双模式完整答案——单次检索自陈三处"无法判断"，分解检索四问全答 |
| `first_run_truncated_log_utf8.txt` | 首跑（21:27）完整轨迹的 UTF-8 转码副本：控制台缓冲在 agentic 第 3 轮截断（compare 模式不落盘，后半段失传），含 NON-AGENTIC 答案与 agentic 前两轮分解检索轨迹 |

命令、汇总表与结论见 `task1.md` ③3.2。语料：offline BM25（21,372 法条分块 / 288 篇文档）。

## 不含密钥

已扫描全部文件：无 API key 值、无 `sk-`／`Bearer` 凭据模式命中；密钥仅存在于未入库的 `.env`。

## 校验方法

`certutil -hashfile <文件> SHA256`（Windows）或 `sha256sum <文件>`，与同目录 `SHA256SUMS.txt` 比对。
