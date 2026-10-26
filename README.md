# 工作个人 AI 化（Cursor Skill）

把「先查再答 + 验收后回写 + 随手 ADD 入库」固定成可重复流程，让 AI 越用越懂你。

## 三条命令

| 命令 | 作用 |
|---|---|
| `ASK …` | 先查文档桶再答；查不到就说没有 |
| `WRITEBACK` / 「回写经验」 | 人确认后把经验写进文档桶 |
| `ADD …` | 半开放分类入库；默认五桶，对不上才提议新建 |

硬规则：禁止编造文档内容；任何写入必须人确认。

## 默认五桶

关于我 / 本周事实墙 / 做事方法 / 经验与踩坑 / 规矩

本仓库 `buckets/` 是空模板；也可指向你自己的本地目录或腾讯文档（见 Skill 正文）。

## 安装（Cursor）

### 方式 A：项目内 Skill（推荐先试）

把本仓库克隆进你的项目，或把 `.cursor/skills/work-personal-ai/` 整夹拷进项目的 `.cursor/skills/`：

```bash
git clone https://github.com/wuzhuo01/work-personal-ai.git
cp -R work-personal-ai/.cursor/skills/work-personal-ai <你的项目>/.cursor/skills/
```

在该项目里打开 Cursor Agent，说「按工作个人 AI 化」或 `ASK …`。

### 方式 B：用户级 Skill

把 `SKILL.md`（及同目录辅助文件）放到 Cursor 用户 skills 目录（以你本机 Cursor 版本文档为准），重启或新开 Agent 会话后触发同上。

### 方式 C：Grok Bot

由本人确认后，用 UpdateSkill 把 `SKILL.md` 正文写入全局 skills（**不要在未确认时代装**）。

## WorkBuddy 备选

若不支持 Skill 文件：把 [`workbuddy-规矩页可贴版.md`](./workbuddy-规矩页可贴版.md) 贴进腾讯文档「5-规矩」页，每次开头说「按规矩页来」。

## 触发词

- 「按工作个人 AI 化」「按规矩来」
- `ASK …` / `ADD …` / `WRITEBACK`

## 文档与依赖

- Skill 正文：[`SKILL.md`](./SKILL.md)（与 `.cursor/skills/work-personal-ai/SKILL.md` 同步）
- 本地桶模板：[`buckets/`](./buckets/)
- 腾讯文档种子页文件夹：https://docs.qq.com/desktop/mydoc/folder/MpCvMVUvDFew
- 默认稳妥路径：读写本地 Markdown；腾讯文档 MCP 可用时可选双写

## 许可

MIT
