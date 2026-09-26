# 实验 6-2 · async-agent（Flux 异步框架）

对应 `task3.md` ③ 3.2。agent 代跑（用户 2026-09-25 授权："跑5-10,6-2实验"），LLM 场景模型＝`deepseek-v4-flash`（百炼额度耗尽后的改线，见 ② 2.3 步骤 0）。

## 收录范围

| 文件/目录 | 内容 | 对应本子 |
|---|---|---|
| `offline-demos-20260925b.txt` | 三个离线演示全绿：①并行 vs 串行**加速比 3.00×**（4.50s→1.50s）②打断冻结 T1/T2/T3＝33%/22%/11%＋恢复后 T4 完成 ③检查点 3 事件/2 任务跨会话还原一致 | ③3.2 表 |
| `real-experiment-20260925b.txt` | `run_real_experiment.py --tick-real 0.15` exit=0，输出证据目录路径（收据本体见 `validation-receipts/`） | ③3.2"真实实验" |
| `scenarios-all-20260925.txt` | 四个 LLM 场景全过（deepseek-v4-flash＋真实子进程）：①即时提问不阻塞 ②积压指令批量处理出 HTML＋日语总结 ③"取消"即时杀 T1（36%）④三脚本竞速＋50% 阈值取消＋整合报告 | ③3.2 四场景逐条 |
| `validation-receipts/` | `run_real_experiment` 落盘收据原样复制（`manifest.json`、`protocol.json`、`summary.json`、4 份场景 JSON、2 份 artifacts）——含任务 pid、进度、sha256 收据 | ③3.2 证据级条目 |

> 未收录：`scenario1-probe-20260925.txt`（沙箱 WinError 5 边界实录，属运行环境排错记录，索引见 `task3.md` ③ 3.4 本地 `_agent_runs\` 路径）；分析输入 `book/chapter4.md` 属上游书稿，不入库。

## 复跑方式

`task3.md` 2.3 步骤表（六步；离线三演示零 key，LLM 场景读实验目录 `.env`——不入库）。注意：实验内真实子进程需 stdout 管道，在受限沙箱按 `AGENTS.md` 规则 8⑤ 需一次性放宽（或在 IDE/终端跑）。

## 密钥与校验

- **不含任何密钥**：日志与收据只含模型名、任务 pid、哈希与进度；`.env` 在白名单外（`.gitignore` 显式拒绝）。上传前双模式扫描零命中。
- 校验：`certutil -hashfile <文件名> SHA256` 与 `SHA256SUMS.txt` 首段比对。
