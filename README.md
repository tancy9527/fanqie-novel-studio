# 🖋️ 番茄小说工作室 · fanqie-novel-studio

[English](./README.en.md) | 中文

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg?style=flat-square)](LICENSE)
[![DSH](https://img.shields.io/badge/DSH-%E2%89%A50.1.1--rc.2-4b8bbe.svg?style=flat-square)](https://github.com/deepseek-ai/deepseek-harness)
[![Skills](https://img.shields.io/badge/Agent%20Skills-%E5%85%BC%E5%AE%B9-orange.svg?style=flat-square)](https://agentskills.io)

**把一套经过真实长篇验证的网文创作工艺，打包成一个任何人都能下载、任何 AI 环境都能用的 skill。**

一个 skill 就是一个文件夹里的 `SKILL.md`（YAML frontmatter + 指令）。AI 遇到「写小说 / 评分卡 / 世界观设定 / 章末钩子 / 改稿」这类任务时动态加载它，照着里面的工艺写、评、改。本 skill 把整条流程固化下来：**建世界观 → 定大纲 → 逐章写（带评分卡）→ 改稿学习 → 平台发布**。

## 它解决什么问题

| 你的困扰 | 这里给的答案 |
|---|---|
| 世界观越写越乱，AI 自己乱编设定 | **一问一答设定法**：把待补设定拆成 50–100 问，每题附候选答案，作者逐条「选/改/自答」，确认一条才转正一条——AI 不许单方面定稿 |
| 不知道一章写成什么样算合格 | **章节评分卡**：11 个字段 + 五维加权（25/25/20/15/15）+ 爽点 ★1–4 分级 + 硬封印 7 条 + 章节类型封顶（铺垫 4.0 / 常规 4.5 / 爆发 5.0），星级不许拍脑袋 |
| 读者追读往下掉 | **章末钩子硬标准 8 条**：爽点预告驱动、落点四选一、结尾四禁（太圆/太虚/太解释/宣告计划）、断章三式 |
| 节奏太慢、铺垫成章 | **节奏硬规则**：一章至少见血或见钱、三章内动手、五章内打脸、开头两段进事、信息一次给完 |
| AI 写出来的没「我的味道」 | **番茄改稿对比学习**：作者改稿发回 → 逐处拆解删/改/加 → 沉淀成可复现的改稿规范，写新章前必读 |
| 一章 2500 字总是写不够 | **场景级细纲法**：把一章拆成 3–4 个场景（目标/人物/对话/情绪落点/字数），字数不足的根因就是细纲没拆到场景级 |
| 评论区没热度 | **评论诱导五选一**：两难选择 / 信息差 / 误解不解释 / 配角高光 / 道德灰区——给评论区埋立场分裂 |
| 设定厚了读者看不懂 | **读者友好层**：每条厚设定配「读者版一句话 + 幕后细则表 + 正文呈现三原则」（怪象先行、设定后行） |

## 两个版本

| 版本 | 位置 | 依赖 | 适用 |
|---|---|---|---|
| **公开版** | 仓库根 `SKILL.md` | 无（纯 Markdown 文件工作流） | Claude Code / Cursor / SkillHub / 任意 LLM 环境 |
| **DSH 版** | `DSH版/SKILL.md` | DSH + `dsh-novel-writer` 插件（novel_* 工具） | DeepSeek Harness 用户：词表/数值/语义/审计全部工具化 |

两版工艺内容一致，区别只在「工具层」：公开版用纯文件工作流（§6 数据层文件约定），DSH 版内置 novel_* 工具映射表。

## 安装

### DSH（DeepSeek Harness）

1. （可选但推荐）安装插件 `dsh-novel-writer`，让工艺里的词表/数值/语义/审计步骤全部自动化；
2. 把 `DSH版/SKILL.md` 所在文件夹放进技能目录（新会话自动发现）：
   - 项目级：`<工作区>/.dsh/skills/fanqie-novel-studio/SKILL.md`
   - 用户级：DSH 用户技能目录（`~/.dsh/skills/fanqie-novel-studio/SKILL.md`）
3. 新会话里命中触发词（写小说 / 续写 / 评分卡 / 世界观设定 / 章末钩子 / 网文章节 等）即自动加载，也可直接点名调用。

```bash
git clone <本仓库地址> "$HOME/.dsh/skills/fanqie-novel-studio"
```

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone <本仓库地址> ~/.claude/skills/fanqie-novel-studio
```

（仓库根即公开版，Claude Code 直接用；不需要 DSH 子目录。）

### Cursor

把根目录 `SKILL.md` 放入项目 `.cursor/rules/`，或使用 skills 目录。

### SkillHub / 其他环境

直接提交本仓库（SKILL.md + README.md），按平台规范补充元信息；任何支持「技能文件作为系统提示词注入」的环境，把 `SKILL.md` 全文作为项目规则注入即可。

## 使用方式（两件套模式）

- **写某本书的章节**：书级 skill（该书的必用词/世界观/人物/改稿规范）+ 本 skill（工艺层）；
- **新开一本书**：先用「一问一答设定法」把世界观与词表建起来，再沉淀书级 skill；
- **只问工艺问题**（评分卡/钩子/节奏）：直接用本 skill。

## 内容速览

1. 全局流程总览：建书 → 世界观 → 大纲 → 分章写 → 改稿 → 发布
2. 世界观设定·一问一答法：问答清单 → 逐批提问（附候选答案）→ 答录跟踪 → 已确认结论 → 转正 → 读者友好层
3. 章节写作工艺：文件结构三块（评分卡+正文+章节备注）→ 评分卡 11 字段与星级判据 → 章末钩子硬标准 8 条 → 节奏硬规则 → 评论诱导五选一 → 写前/写中/写后/收尾
4. 番茄改稿对比学习：原稿 vs 改稿 → 可复现规律 → 沉淀书级改稿规范
5. 平台适配：发布节奏 / 红线自查 / 追读
6. 工具层：公开版=数据层文件约定；DSH 版=novel_* 工具映射表
7. 批次与会话管理：4 章一批 / 单会话 12 章 / 规范永远最新

## 目录结构

```
fanqie-novel-studio/
├── SKILL.md        # 公开版（无插件依赖，标准 Agent Skills 格式）
├── README.md       # 本说明（中文）
├── README.en.md    # English
├── LICENSE         # MIT
└── DSH版/
    ├── SKILL.md    # DSH 版（novel_* 工具映射）
    └── README.md   # DSH 安装说明
```

## 出处

由真实长篇创作过程提炼：世界观 106 问+续问逐条核对、章节评分卡星级体系、番茄草稿箱改稿对比学习。可自由 fork、修改、再发布。

## 许可

[MIT](./LICENSE) © fanqie-novel-studio contributors
