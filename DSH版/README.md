# 番茄小说工作室（DSH 版）

网文长篇创作全流程 skill：世界观一问一答设定法、章节评分卡工艺、章末钩子硬标准、节奏硬规则、评论诱导、写前中后流程、番茄改稿对比学习、批次管理，并内置 `dsh-novel-writer` 插件（novel_* 工具）的调用映射。

## 适用环境

- **DSH**（DeepSeek Harness）会话
- 依赖插件：**dsh-novel-writer**（提供 novel_books / novel_chapter_brief / novel_lexicon / novel_plot / novel_settings / novel_summary / novel_continuity_check / novel_style_check 等工具）

## 安装

把 `SKILL.md` 所在文件夹（`fanqie-novel-studio`）复制到技能目录：

- 项目级：`<工作区>/.dsh/skills/fanqie-novel-studio/SKILL.md`
- 用户级：DSH 用户技能目录（如 `~/.dsh/skills/fanqie-novel-studio/SKILL.md`）

重启/新开会话后，技能目录里会出现 `fanqie-novel-studio`；用户请求命中触发词（写小说/评分卡/世界观设定/章末钩子/网文章节等）即自动加载，也可手动点名调用。

## 使用方式（两件套模式）

| 场景 | 用哪个 |
|---|---|
| 写某一本书的章节 | 本书**书级 skill**（含必用词/世界观/人物/改稿规范）+ 本 skill（工艺层） |
| 新开一本书、还没书级 skill | 本 skill + 先用 §2 一问一答法把世界观/词表建起来，再沉淀书级 skill |
| 只问工艺问题（评分卡/钩子/节奏） | 本 skill |

## 目录结构

```
fanqie-novel-studio/
├── SKILL.md      # 工艺总纲（7 节）
└── README.md     # 本说明
```

## 与公开版的区别

| | DSH 版 | 公开版 |
|---|---|---|
| 工具层 | novel_* 插件工具（词表/数值/语义/审计自动化） | 纯 Markdown 文件工作流 |
| 依赖 | DSH + dsh-novel-writer | 无 |
| §6 | 工具映射表 | 数据层文件约定 |

## 出处

由《我占了大能的化身，还能加点》的真实创作过程（世界观 106 问+续问逐条核对、评分卡体系、番茄改稿对比学习）提炼而来，作者 2026-10 拍板沉淀。
