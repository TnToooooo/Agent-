# 实验 5-10 · erp-agent（NL→SQL，Artifact 模式）

对应 `task3.md` ③ 3.1。agent 代跑（用户 2026-09-25 授权："跑5-10,6-2实验"）。

## 收录范围

| 文件 | 内容 | 对应本子 |
|---|---|---|
| `gold-20260924.txt` | `demo.py gold` 离线自检：10 条人工金标 SQL 逐题执行＋独立参照判分，**10/10（100%）** | ③3.1 表第 1 行 |
| `run-online-deepseek-20260925.txt` | `demo.py run` 在线真跑（**deepseek-v4-flash**）：10 题"生成 SQL→执行→参照判分"，**9/10（90%）**；Q1 失败细节（`date('now')` vs `date('now','localtime')`，885.35 vs 886.2）逐题在内 | ③3.1 表第 2 行＋Q1 剖析 |
| `run-online-20260924.txt` | 首跑收据：百炼 `qwen3.7-plus` 403 `AllocationQuota.FreeTierOnly` 十题全拒（账号级免费额度耗尽原始报错） | ③3.1 模型切换链第 1 环 |
| `run-online-flash-20260925.txt` | 次跑收据：`qwen3.7-flash` 同样 403（证明非单模型额度问题） | ③3.1 模型切换链第 2 环 |

## 复跑方式

`task3.md` 2.2 步骤表（PyCharm：Script path＝`demo.py`，Parameters 见表，Working directory＝本实验目录）；`OPENAI_MODEL` 当前为 `deepseek-v4-flash`（`.env` 不入库）。

## 密钥与校验

- **不含任何密钥**：日志只出现模型名与端点变量名；`.env` 在白名单外（`.gitignore` 显式拒绝）。上传前双模式扫描（`sk-` 前缀／`KEY=` 实值）零命中。
- 校验：`certutil -hashfile <文件名> SHA256` 与 `SHA256SUMS.txt` 首段比对。
