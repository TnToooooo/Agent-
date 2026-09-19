# 实验 2-10 运行证据（上下文压缩策略对比）

## 收录范围

本人 2026-09-19 三次实跑的结果 JSON，由 `ai-agent-book/chapter2/context-compression/experiment.py` 生成（每策略一条记录：成败／迭代／工具调用／tokens／压缩率／溢出）：

| 文件 | 跑次 | 模型 | 说明 |
|---|---|---|---|
| `experiment_20260919_155206.json` | 第 1 跑 | deepseek-v4-flash | 推理白名单补丁**前**；4/6 臂出现"摘要 0 字符"→ 15 轮无终答 |
| `experiment_20260919_171222.json` | 第 2 跑 | deepseek-v4-flash | 白名单补丁（加 `"deepseek"`）后重跑，1/6 成功 |
| `experiment_20260919_185046.json` | 第 3 跑 | glm-5.3-flash | provider 切 zhipu，白名单补 `"glm"`，3/6 成功 |

三跑共同配置：mock 检索（未配 SERPER_API_KEY）、CONTEXT_WINDOW_SIZE=128K、MAX_ITERATIONS=15。四跑汇总表与有据结论见 `task1.md` ③3.1。

## 代码补丁声明

第 2、3 跑证据产生于**本地补丁后**的代码：`compression_strategies.py` 的 `_reasoning_safe_max_tokens` 推理预算白名单加入了 `"deepseek"` 与 `"glm"`（原因：这两个模型输出 `reasoning_content`，占满摘要预算导致摘要为空）。作者原件备份为本地 `compression_strategies.py.bak-agent-20260919`，未上传。第 1 跑为补丁前的原始行为。

## 不含密钥

已扫描全部文件：无 API key 值、无 `sk-`／`Bearer` 凭据模式命中；密钥仅存在于未入库的 `.env`。

## 校验方法

`certutil -hashfile <文件> SHA256`（Windows）或 `sha256sum <文件>`，与同目录 `SHA256SUMS.txt` 比对。
