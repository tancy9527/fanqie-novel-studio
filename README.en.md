# 🖋️ fanqie-novel-studio — a complete web-novel chapter craft skill

[中文](./README.md) | English

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg?style=flat-square)](LICENSE)
[![DSH](https://img.shields.io/badge/DSH-%E2%89%A50.1.1--rc.2-4b8bbe.svg?style=flat-square)](https://github.com/deepseek-ai/deepseek-harness)
[![Skills](https://img.shields.io/badge/Agent%20Skills-compatible-orange.svg?style=flat-square)](https://agentskills.io)

**A battle-tested web-novel writing workflow, packaged as a reusable skill that works in any AI environment.**

A skill is just a folder with a `SKILL.md` (YAML frontmatter + instructions). The agent loads it on demand when a task matches — writing novels, scoring chapters, worldbuilding, chapter hooks, revision. This skill freezes the whole pipeline: **worldbuilding → outline → chapter-by-chapter writing (with a scoring card) → revision learning → platform release**.

## What it solves

| Your problem | What this skill gives you |
|---|---|
| Worldbuilding drifts, the AI invents canon | **Q&A worldbuilding method**: split open questions into 50–100 items, each with 2–4 candidate answers; the author picks/edits/answers each one, and only confirmed items are promoted to canon — the AI never finalizes settings unilaterally |
| No idea what a "good chapter" means | **Chapter scoring card**: 11 fields + weighted 5-dimension scoring (25/25/20/15/15) + ★1–4 payoff grading + 7 hard seals + per-type score caps (setup ≤4.0 / normal ≤4.5 / climax 5.0) — stars are never guessed |
| Reader retention drops | **8 chapter-end hook rules**: payoff-preview driven, 4 landing types, 4 forbidden endings, 3 cut points |
| Pacing too slow, filler chapters | **Pacing hard rules**: every chapter draws blood or money, a fight within 3 chapters, a payoff within 5, no more than 2 opening paragraphs before the story starts |
| AI output doesn't feel like "you" | **Revision comparison learning**: when the author's edited chapters come back, diff them line by line and distill reproducible style rules into a book-level style spec |
| Can't hit 2500 words per chapter | **Scene-level outlining**: split each chapter into 3–4 scenes (goal/characters/dialogue/emotion/word count) — the root cause of short chapters is one-line outlines |
| Empty comment sections | **Comment bait (pick one of five)**: dilemma / information gap / unexplained misunderstanding / supporting-character highlight / moral gray area |
| Deep lore confuses readers | **Reader-friendly layer**: every thick setting ships with a one-line reader version + a behind-the-scenes table + three presentation rules (anomaly first, explanation later) |

## Two editions

| Edition | Location | Dependencies | For |
|---|---|---|---|
| **Public** | `SKILL.md` at repo root | None (plain Markdown file workflow) | Claude Code / Cursor / SkillHub / any LLM environment |
| **DSH** | `DSH版/SKILL.md` | DSH + `dsh-novel-writer` plugin (novel_* tools) | DeepSeek Harness users: lexicon/number/semantic/audit steps become tool calls |

Same craft in both editions; only the tool layer differs — the public edition is a pure file workflow (§6 data-layer conventions), the DSH edition maps every step to novel_* tools.

## Install

### DSH (DeepSeek Harness)

1. (Optional, recommended) install the `dsh-novel-writer` plugin to automate lexicon/number/semantic/audit steps;
2. Put the `DSH版/SKILL.md` folder into a skills directory (auto-discovered in new sessions):
   - project: `<workspace>/.dsh/skills/fanqie-novel-studio/SKILL.md`
   - user: `~/.dsh/skills/fanqie-novel-studio/SKILL.md`
3. In new sessions it loads automatically on trigger words (write a novel / continue / scoring card / worldbuilding / chapter hooks…) or when named explicitly.

```bash
git clone <this repo> "$HOME/.dsh/skills/fanqie-novel-studio"
```

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone <this repo> ~/.claude/skills/fanqie-novel-studio
```

(The repo root is the public edition; the DSH subfolder can be ignored.)

### Cursor

Put the root `SKILL.md` into `.cursor/rules/` or your skills directory.

### SkillHub / other agents

Submit this repo (SKILL.md + README.md) per the platform's metadata conventions. Any environment that supports injecting a skill file as system prompt can just use `SKILL.md` as project rules.

## Usage (two-layer pattern)

- **Writing chapters for a specific book**: book-level skill (lexicon/worldview/characters/style spec of that book) + this skill (craft layer);
- **Starting a new book**: build the worldbook and lexicon with the Q&A method first, then distill a book-level skill;
- **Craft questions only** (scoring card / hooks / pacing): use this skill directly.

## Contents at a glance

1. Pipeline overview: build book → worldbuilding → outline → chapter writing → revision → release
2. Q&A worldbuilding method: question list → batched questions with candidate answers → answer log → confirmed conclusions → promotion to canon → reader-friendly layer
3. Chapter craft: 3-part file structure (scoring card + body + chapter notes) → 11-field scoring card → 8 hook rules → pacing hard rules → comment bait → pre/write/post/wrap-up
4. Revision comparison learning: original vs edited → reproducible rules → book-level style spec
5. Platform fit: release cadence / red lines / retention
6. Tool layer: public = file conventions; DSH = novel_* tool mapping
7. Batch & session management: 4 chapters per batch / ~12 chapters per session / specs are always the latest version

## Repo layout

```
fanqie-novel-studio/
├── SKILL.md        # Public edition (standard Agent Skills format, zero deps)
├── README.md       # 中文
├── README.en.md    # English (this file)
├── LICENSE         # MIT
└── DSH版/
    ├── SKILL.md    # DSH edition (novel_* tool mapping)
    └── README.md   # DSH install guide
```

## Provenance

Distilled from a real long-form project: a 106-question worldbuilding Q&A (plus follow-ups), the chapter star-rating system, and tomato-platform revision comparison learning. Free to fork, modify, and republish.

## License

[MIT](./LICENSE) © fanqie-novel-studio contributors
