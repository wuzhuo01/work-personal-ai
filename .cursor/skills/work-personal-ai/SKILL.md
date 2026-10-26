---
name: work-personal-ai
version: 0.1.0
display_name: 工作个人AI化
display_name_en: Personal Work AI
description: Use when the user says 按工作个人 AI 化 / 按规矩来, or runs ASK / ADD / WRITEBACK: look up personal doc buckets first, write back only after human confirm, classify into five default buckets.
description_zh: 先查文档桶再答（ASK）、人确认后回写经验（WRITEBACK）、半开放分类入库（ADD）。查不到就说没有；写入必须人确认。
description_en: Look up personal doc buckets before answering (ASK), write back only after human confirm (WRITEBACK), and classify notes into five default buckets (ADD). Never invent document content.
---
# 工作个人 AI 化

把「先查再答 + 验收后回写 + 随手 ADD 入库」固定成可重复流程。事实只进文档桶，不进本 Skill。

## 文档桶（默认五桶，半开放）

本地镜像（默认读写）：优先本仓库 `buckets/`；也可改为你机器上的固定目录（如 `/workspace/外脑/工作个人AI化/`）。路径以你安装后的实际位置为准。

| 桶 | 本地文件 | 腾讯文档 file（可选同步） |
|---|---|---|
| 关于我 | `1-关于我.md` | https://docs.qq.com/doc/DTVh6dVpVaXp2TnBF |
| 本周事实墙 | `2-本周事实墙.md` | https://docs.qq.com/doc/DTXJxR25WaXF6bEN6 |
| 做事方法 | `3-做事方法.md` | https://docs.qq.com/doc/DTUt3Y3pXV0N3VWtU |
| 经验与踩坑 | `4-经验与踩坑.md` | https://docs.qq.com/doc/DTWJ6WEtEQ0RGWW9S |
| 规矩 | `5-规矩.md` | https://docs.qq.com/doc/DTWRGQXhIZHpqdnhz |

文件夹：https://docs.qq.com/desktop/mydoc/folder/MpCvMVUvDFew

**读写优先级（稳妥路径）**

1. **默认**：读写本地 Markdown 镜像（Cursor / 无 MCP 时也能跑）。
2. **可选**：若当前环境已连接腾讯文档 MCP，ASK 可先 `get_content` / `doc.find` 读对应页；WRITEBACK / ADD 在人确认后，除写本地外，可用 `doc.get_last_operable_pos` + `doc.insert_markdown`（或 `doc.insert_paragraph_with_text`）追加到腾讯文档页。两边冲突时以用户指定为准；未指定则本地为准并提醒「腾讯文档未同步」。
3. 新建桶：先提议桶名 + 理由，**不自动建**；人同意后再建本地文件，并（可选）在腾讯文档文件夹建页、更新 `README.md` 索引。

## 硬规则（始终生效）

- 查不到就说查不到；禁止编造「文档里写过」。
- 任何写入（ADD / WRITEBACK / 新建桶）必须人确认后再落盘。
- 不在本 Skill 里塞会过期的事实正文。
- 女儿相关、隐私敏感内容入库前必须用户明确同意，并按要求匿名化。

## 触发

- 用户说「按工作个人 AI 化」「按规矩来」，或显式调用本 Skill
- 或命令：`ASK …`、`ADD …`、`WRITEBACK` / 「回写经验」

---

## 命令 1：ASK（先查再答）

1. 读用户问题，判断可能相关的文档桶（可多桶）。
2. **先查**：在对应文档里检索/阅读相关段落；摘出与问题直接相关的原文要点（带出处页名）。本地用 Read / 搜索；腾讯文档可用则再读一遍补漏。
3. **再答**：
   - 有摘录：必须基于摘录 + 模型能力生成；回答里简短标明「依据：××页」。
   - 无摘录：明确说「文档里没有找到对应内容，下面按通用能力答」，再回答；不得假装查过。
4. 答完后主动问一句：「要不要把这次有用的做法/坑回写进经验？」用户说要再走 WRITEBACK。

## 命令 2：WRITEBACK（验收后回写经验）

1. 仅在用户确认「可以回写」后执行（或用户直接说 WRITEBACK）。
2. 起草一条短记录：
   - 场景：
   - 做法/结论：
   - 下次注意：
   - 建议归属：经验与踩坑（默认）或其它桶
3. 展示草稿，等用户确认或改一句。
4. 确认后再写入目标文档（本地必写；腾讯文档按上方可选同步）；未确认不落盘。

## 命令 3：ADD（随手灌知识，独立于提问）

1. 用户：`ADD` + 粘贴一段内容（或附件要点）。
2. AI 给出建议：
   - 建议进哪一桶（优先用默认五桶）
   - 一句话摘要
   - 若都不合适：提议新建桶名 + 理由（**不自动建**）
3. 用户确认（或改桶 / 同意新建）后再写入。
4. 分类原则：半开放——默认五桶优先；对不上才提议新建；禁止一次输入拆成很多琐碎新桶。

## WorkBuddy 备选

若环境吃不了 Skill 文件：把同目录 `workbuddy-规矩页可贴版.md` 全文贴进「5-规矩」页，用户每次开头说「按规矩页来」。
