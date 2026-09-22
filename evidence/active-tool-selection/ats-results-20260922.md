# active-tool-selection 实跑结果（转录自 2026-09-22 运行输出）

> 说明：三步运行的原始输出直出控制台（按沙箱规程未做文件重定向），本文件为**逐表转录版**，数字与运行输出逐一对齐；额度相关过程收据见同目录 `03-compare-400-receipt.txt`。对应 `task2.md` ③ 主跑二各表。

## ① `--offline`（零 key、确定性；10 任务、35 工具目录、top-k=5）

| Strategy | Tools in context | Schema tokens | Recall (gold reachable) |
|---|---|---|---|
| all-tools | 35 | 3,857 | 100% |
| retrieval top-5 | 5 | 517 | 100% |

=> retrieval 保 100% recall 同时省 **86.6%**（3,857→517），10/10 任务 gold 全命中。

Scaling（目录 35→50→100→200→400，all / retrieval tokens）：
3,857→517 ／ 5,342→522 ／ 10,292→522 ／ 20,258→522 ／ 40,258→522；recall 恒 100%。

## ② `--strategy compare`（qwen-plus，10 任务 × 3 策略）

| Strategy | Accuracy (calls gold) | Avg tools in ctx | Avg tokens | Avg latency |
|---|---|---|---|---|
| all-tools | 90% | 35 | 10,352 | 5.88s |
| retrieval | 80% | 4.7 | 1,747 | 3.88s |
| active (MCP-Zero) | 50% | 4.8 | 6,579 | 16.12s |

> 留档：② 首跑（qwen3.7-plus）曾得 all 60%／retrieval 60%／active 40%（9,624／1,917／5,617 tok；7.93／6.55／13.51s），因该模型免费额度耗尽后按统一口径重跑为上表。

## ③ `--strategy compare --num-tools 400`

离线段（400 工具目录、top-k=5）：

| Strategy | Tools in context | Schema tokens | Recall |
|---|---|---|---|
| all-tools | 400 | 40,258 | 100% |
| retrieval top-5 | 5 | 522 | 100% |

=> 省 **98.7%**（40,258→522），10/10 任务 gold 命中（Monitor service 行 retrieved 含 svc2_op* 合成干扰项仍命中 devops_monitor）。

在线段（qwen-turbo，10 任务 × 3 策略）：

| Strategy | Accuracy (calls gold) | Avg tools in ctx | Avg tokens | Avg latency |
|---|---|---|---|---|
| all-tools | 70% | 400 | 68,326 | 3.01s |
| retrieval | 100% | 4.8 | 1,677 | 1.32s |
| active (MCP-Zero) | 50% | 3.5 | 1,646 | 1.42s |

## 备注

- 400 工具下 all 每任务 68,326 token＝retrieval 的 40.7×，准确率反降（70% vs 100%）——p.116"规模伤害正确性"实证。
- ②与③在线段模型不同（qwen-plus / qwen-turbo，免费额度所致）：token 爆炸与 schema 规模相关、模型无关（离线段已证）；准确率跨表比较含模型因素。
- 工具执行为模拟（作者设计：只测"选没选对"）。
