---
title: OpenSpec
type: concept
tags: [ai-coding, agent-workflow, spec-driven, planning]
created: 2026-04-29
updated: 2026-04-29
sources:
  - raw/openspec-official-docs-excerpt.md
status: draft
---

# OpenSpec

**一句话**：spec-driven AI coding 工作流——**代码写之前，先让人和 agent 在 markdown 里对齐**（为什么做、改什么、怎么改、拆成哪些任务）。由 fission-ai 维护。官方仓库：<https://github.com/fission-ai/openspec>。

## 为什么 AI PM 该关注

- Agent 跑偏的根因几乎全在"没对齐就开工"。OpenSpec 把对齐**显式化、可审阅、可版本控制**。
- PM 本来就在做的事（写 PRD、拆任务、对齐 scope）——OpenSpec 把它变成 agent 能直接读懂的结构。
- 尤其适合**存量项目加 feature**：`openspec/specs/` 沉淀系统当前真相，`openspec/changes/` 描述 delta，实现完成后 delta 回写 specs——spec 始终代表系统现状，不会和代码脱节。
- **你的主战场在 review，不在 apply**。

## 目录结构（长在目标项目根）

```
openspec/
├── project.md              # 项目上下文（写给 agent 看）
├── AGENTS.md               # agent 指令
├── specs/                  # 当前上线能力（canonical）
│   └── <capability>/
│       ├── spec.md         # WHAT + WHY
│       └── design.md       # HOW（可选）
└── changes/                # 提案中的改动
    ├── <change-name>/
    │   ├── proposal.md     # 为什么、改什么、影响
    │   ├── tasks.md        # 实现 checklist
    │   ├── design.md       # 技术决策（可选）
    │   └── specs/          # 改动后的 spec 状态
    └── archive/            # 完成归档
        └── YYYY-MM-DD-<name>/
```

## 四步工作流

| # | 命令 | 目的 | PM 投入 | Agent 投入 |
|---|---|---|---|---|
| 1 | `/opsx:propose <name>` | 把 1-2 句 feature 描述展成完整对齐包：proposal + specs + design + tasks | 给简短描述 + 上下文 | **生成四件套初稿** |
| 2 | — (人工) | **改 markdown 到每句你都认账**。整个流程含金量最高的 30 分钟 | **主角**——逐句审、划边界、补非目标 | 按反馈调整 |
| 3 | `/opsx:apply` | Agent 按 `tasks.md` 逐项实现，每项勾掉一个复选框 | 每 3-5 task spot-check 一次 | **主角**——写代码 |
| 4 | `/opsx:archive` | Sync delta specs 回 canonical + 移文件夹到 `archive/YYYY-MM-DD-<name>/` | 先跑 `/opsx:verify` 查潜在问题 | 合 specs + 移文件 |

> 其他命令：`/opsx:new <name>` 创建最小 scaffold（只有 metadata）、`/opsx:continue` 往后生成一个 artifact、`/opsx:ff` 快进创建所有 artifact、`/opsx:verify` 归档前自检。

## Step 2 是 PM 的主战场——review 清单

拿到 propose 后的四件套，逐个审：

### `proposal.md`
- 问题表述是**真问题**吗？不是"老板说要做"？
- 用户 / 业务价值一句话说得清吗？
- **非目标（out-of-scope）列了吗**？——经常被省，但最容易让 agent 跑偏
- 成功标准可量度吗？

### `specs/<capability>/spec.md`
- 每条 SHOULD 语句**可验证**吗？
- 边界条件（空、超量、异常、并发、错误恢复）覆盖了吗？
- 和现有 specs 的差异点写清楚了吗？
- 有没有把"实现细节"塞进 spec（应该放 design.md）？

### `design.md`
- 选 A 不选 B 的理由写了吗？
- 对现有架构 / 数据模型的**假设**写明了吗？
- 有没有落下兼容 / 迁移细节？

### `tasks.md`
- 每个 task 能**独立 review / 独立回滚**吗？
- 顺序对吗？（先建 schema，再调 handler，别反了）
- 粒度合适吗？——太粗 agent 会迷，太细浪费

**发现跑偏：改 spec / tasks，不要改代码。spec 是真相。**

## 快速起手 checklist（存量项目 + 加 feature）

- [ ] 检查项目根有没有 `openspec/`；没有就按 [官方 README](https://github.com/fission-ai/openspec) init
- [ ] 填 `openspec/project.md`——让 agent 知道项目上下文 / 技术栈 / 关键约束
- [ ] 检查 `openspec/AGENTS.md`——agent 行为约定
- [ ] 想好 feature 名字（kebab-case，如 `add-dark-mode`、`export-csv-report`）
- [ ] `/opsx:propose <name>`
- [ ] **坐下来改四件套到认账**（含金量最高的 30 分钟，不要省）
- [ ] `/opsx:apply`，每 3-5 个 task 停下来 spot-check
- [ ] 跑 `/opsx:verify` → `/opsx:archive`
- [ ] 回到 `Our AI Age` 让 LLM 做**第二次 ingest**：新增 `raw/openspec-<feature>-practice.md`，更新本页"待填"区

## 待填（等用户实战后 ingest 回来）

留白区——方法论要求 wiki 不伪造体验。跑完一次实战再回来补这些：

- 第一次写 proposal 踩的坑（题目太大？太小？漏了非目标？）
- spec "粒度合适"的体感是什么（WHAT vs HOW 的边界在哪里最舒服？）
- apply 阶段 agent 跑偏的典型模式（哪几类任务 agent 特别容易误解？）
- 继续用 vs 换方法的判断
- 和其他 spec-first / planning 工具的印象对比（PRP、Spec-Kit、自家 PRD 模板等）

## 常见疑问（基于官方文档能回答的部分）

**Q: 已经有 PRD 了，再写 proposal 是不是重复？**
不是——proposal 受众是 agent，格式是 agent 消费友好的；PRD 受众是人 + 利益相关方。可以把 PRD 里的结论 paste 进 proposal 作为前情，但不等同。

**Q: 必须用 `design.md` 吗？**
官方标注为 optional，针对"技术决策不 trivial"的场景。纯 CRUD / 明确模式的 feature 可以省，但复杂架构决策建议写。

**Q: apply 时 agent 跑一半失败怎么办？**
tasks.md 用复选框跟进度，未完成的 task 保留 `- [ ]`。下次 `/opsx:apply` 继续未完成项。若是 spec 本身错了，改 spec + tasks，不要强行让 agent 按错的写完。

**Q: archive 时发现 delta specs 和实际代码不一致？**
先别 archive。用 `/opsx:verify` 找差异，看是 spec 写漏了还是 agent 实现偏了。spec 是真相——以 spec 为准把代码改齐，或反之改 spec，然后再 archive。

## 出处

- **原项目**：<https://github.com/fission-ai/openspec>（fission-ai 维护）
- **本页所本**：[../raw/openspec-official-docs-excerpt.md](../raw/openspec-official-docs-excerpt.md)
- **拉取方式**：Claude Code Context7 MCP
- **Context7 库 ID**：`/fission-ai/openspec`（reputation: Medium, benchmark: 75.8）
- **拉取日期**：2026-04-29
