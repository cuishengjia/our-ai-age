# CLAUDE.md — Our AI Age 工作规约

> LLM 在这个仓库的操作手册。Claude Code 自动加载到每次会话上下文。方法论原文见 [llm-wiki.md](./llm-wiki.md)。

## 仓库是什么

一名 AI 产品经理的**公开 LLM-wiki**。三层架构：

| 层 | 路径 | 权责 |
|---|---|---|
| Raw sources | `raw/` | 用户 curate，LLM 只读 |
| Wiki | `wiki/` | LLM 创建 + 维护 |
| Metadata | `CLAUDE.md` / `index.md` / `log.md` / `README.md` / `llm-wiki.md` | 混合 |

## 角色分工

- **用户 = curator**：选源、提问、校对关键判断、决定方向。
- **LLM（我）= wiki 维护员 + 综合者**：读源、提炼、写条目、维护交叉引用、标矛盾、更新索引和日志、定期 lint。

## 写作基调

- **语言**：中文为主，英文术语可保留。
- **视角**：一线 AI PM——「能用 / 好用 / 值得用」的判断，不堆砌百科全书。
- **读者**：公开读者（AI 产品从业者、学习者、跨行观察者）。默认不在用户公司。
- **红线**：不写内部公司名、未发布产品细节、敏感 roadmap。每条信息须可公开。

## Wiki 页规范

### 页面类型

| type | 用途 | 例 |
|---|---|---|
| `concept` | 方法、框架、模式 | `openspec.md` |
| `entity` | 产品、公司、人、工具 | `claude-code.md` |
| `synthesis` | 跨条目对比 / 地图 | `agent-tools-对比.md` |
| `observation` | 用户的判断、预测（明确观点） | `2026-ai-pm-差别.md` |

### Frontmatter（必备）

```yaml
---
title: OpenSpec
type: concept            # concept | entity | synthesis | observation
tags: [ai-coding, agent-workflow]
created: 2026-04-29
updated: 2026-04-29
sources:
  - raw/openspec-practice.md
status: draft            # draft | reviewed | stable
---
```

### 文件命名

- kebab-case，英文 slug 优先（URL 友好）：`openspec.md`、`agent-coding-tools.md`
- 中文标题也可：`ai-pm-工具链.md`（GitHub URL 会 URL-encode）

### 交叉引用

- **首选相对路径**：`[OpenSpec](../wiki/openspec.md)` → GitHub + Obsidian 都识别。
- Obsidian `[[wikilinks]]` 可在草稿中用，**公开提交前转相对链接**。
- 引用源：`[source](../raw/openspec-practice.md)`。

## 三个核心操作

### Ingest（进源）

触发：用户丢新源进 `raw/`，或口述一段经验让我整理。流程：

1. **读源**，完整一遍。
2. **对齐 key takeaways**：跟用户确认理解。
3. **写 raw**（若是口述）：`raw/<slug>.md`，第一人称、用户经验、我不加评注。
4. **创建 / 更新 wiki 条目**：可能涉及 10+ 页——核心条目新建或迭代；相关概念页追加证据、矛盾、交叉；综合页更新。
5. **更新 `index.md`**：新条目入目录，已有条目更新一句话摘要。
6. **追加 `log.md`**：`## [YYYY-MM-DD] ingest | <源标题>` + 1-3 句变更摘要。
7. **更新 `README.md` 导航**：若本次 ingest 新增了 wiki 页，在 README 的"最近的条目" / 导航区补上链接。**README 是仓库门面 + 导航页**（用户 2026-04-29 规定），伴随内容增长持续迭代——让读者从首页就能摸到新内容。
8. **commit** 一次 ingest = 一个 commit。

### Query（查问）

1. **先读 `index.md`**，定位相关页。
2. **读 wiki 条目**（不直接回 raw，除非 wiki 不够）。
3. **合成答案 + 引用**，带 `[源](path)` 链接。
4. **回填**：若形成新洞察、对比、地图，**写成 wiki 页**，不要只留在对话里。追加 log。
5. 输出形态不限于 Markdown——表格、Marp 幻灯、图表、canvas 均可。

### Lint（巡检）

触发：用户说 "lint"、或我察觉异常。检查项：

- 条目间矛盾陈述
- 新源未同步到的旧条目
- 孤立页（无入链）
- 频繁提及但缺独立页的概念
- 缺失的交叉引用
- 可用 web search 填补的 data gap

输出：`wiki/lint-report-YYYY-MM-DD.md` 或直接列问题给用户决定。

## log.md 格式

```
## [YYYY-MM-DD] ingest | <源标题>
- 新建 / 更新的文件
- 1-3 句变更摘要

## [YYYY-MM-DD] query | <主题>
- 回填了哪个 wiki 页

## [YYYY-MM-DD] lint
- 详见 lint-report-YYYY-MM-DD.md
```

查最近：`grep "^## \[" log.md | tail`

## Commit 规约

- ingest = 一个 commit，message：`ingest: <源标题>` 或 `docs: add <主题> wiki page`
- lint = `chore: lint pass YYYY-MM-DD`
- 修复 = `fix: ...` / 重构 = `refactor: ...`
- Conventional commits（`feat` / `fix` / `docs` / `chore` / `refactor` / `perf`）
- **不加 Claude 署名**（全局禁用）

## Guardrails

- `raw/` 只读——**不删除、不重写、不改名**现有文件。
- wiki 条目大改前，先向用户说明 diff 让其过目。
- 察觉可能泄露用户雇主内部信息、未发布产品、敏感 roadmap 的线索：**停下问用户**。
- 不自作主张重构目录结构——先提议。

## 演化

本文件跟着使用演化。遇到新场景、发现新惯例就更新这里，并在 log 里记一笔。
