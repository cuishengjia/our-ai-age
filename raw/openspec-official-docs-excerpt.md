# OpenSpec 官方文档 · Context7 摘录

> **raw/ 层文件——LLM 只读，不改动。**

## 来源元数据

- **上游仓库**：<https://github.com/fission-ai/openspec>
- **维护者**：fission-ai
- **拉取方式**：Claude Code 的 Context7 MCP server
- **Context7 库 ID**：`/fission-ai/openspec`
- **Source reputation (Context7)**：Medium
- **Benchmark score (Context7)**：75.8
- **代码片段总数 (Context7)**：309
- **拉取日期**：2026-04-29
- **查询关键词**：`Core workflow for adding a feature to an existing project: init, creating a change proposal, writing spec deltas, tasks.md format, agent handoff, archiving a completed change. Include CLI commands and directory layout.`

以下为 Context7 返回的原文摘录，每段保留上游 GitHub URL。原文以英文为主，未翻译；中文 wiki 页基于此摘录撰写。

---

## Snippet 1 · Initialize a new change scaffold

**来源**：<https://github.com/fission-ai/openspec/blob/main/docs/commands.md>

Use this command to create a new change directory and metadata file. It requires a change name and optionally a schema.

```bash
/opsx:new [change-name] [--schema <schema-name>]
```

```text
openspec/changes/<change-name>/
└── .openspec.yaml    # Change metadata (schema, created date)
```

```text
You: /opsx:new add-dark-mode

AI:  Created openspec/changes/add-dark-mode/
     Schema: spec-driven

     Ready to create: proposal
     Use /opsx:continue to create it, or /opsx:ff to create all artifacts.
```

---

## Snippet 2 · OpenSpec Workflow Example

**来源**：<https://github.com/fission-ai/openspec/blob/main/README.md>

Demonstrates the typical interaction flow with OpenSpec commands for proposing, applying, and archiving changes.

```text
You: /opsx:propose add-dark-mode
AI:  Created openspec/changes/add-dark-mode/
     ✓ proposal.md — why we're doing this, what's changing
     ✓ specs/       — requirements and scenarios
     ✓ design.md    — technical approach
     ✓ tasks.md     — implementation checklist
     Ready for implementation!

You: /opsx:apply
AI:  Implementing tasks...
     ✓ 1.1 Add theme context provider
     ✓ 1.2 Create toggle component
     ✓ 2.1 Add CSS variables
     ✓ 2.2 Wire up localStorage
     All tasks complete!

You: /opsx:archive
AI:  Archived to openspec/changes/archive/2025-01-23-add-dark-mode/
     Specs updated. Ready for the next feature.
```

---

## Snippet 3 · Implement tasks from a change

**来源**：<https://github.com/fission-ai/openspec/blob/main/docs/commands.md>

Reads the tasks.md file and executes implementation steps sequentially. Tracks completion status using markdown checkboxes.

```bash
/opsx:apply [change-name]
```

```text
You: /opsx:apply

AI:  Implementing add-dark-mode...

     Reading tasks.md:
     - [ ] 1.1 Create ThemeContext
     - [ ] 1.2 Add CSS custom properties
     - [ ] 1.3 Implement localStorage persistence

     Working on 1.1: Create ThemeContext...
     [Creates src/context/ThemeContext.tsx]

     ✓ 1.1 Complete

     Working on 1.2: Add CSS custom properties...
     [Updates src/styles/globals.css]

     ✓ 1.2 Complete
     ...
```

---

## Snippet 4 · Archive a Completed Change

**来源**：<https://github.com/fission-ai/openspec/blob/main/docs/commands.md>

Archives a completed change. Finalizes the change and moves it to the archive folder. It checks artifact completion status, task completion (with warnings for incomplete tasks), and offers to sync delta specs if not already synced. The change folder is then moved to `openspec/changes/archive/YYYY-MM-DD-<name>/`, preserving all artifacts for an audit trail.

**Tips（原文）**:
- Archiving will not block on incomplete tasks but will issue a warning.
- Delta specs can be synced during the archive process or beforehand.
- Archived changes are preserved for historical reference.
- It is recommended to use `/opsx:verify` first to catch potential issues.

```text
You: /opsx:archive

AI:  Archiving add-dark-mode...

     Artifact status:
     ✓ proposal.md exists
     ✓ specs/ exists
     ✓ design.md exists
     ✓ tasks.md exists (8/8 tasks complete)

     Delta specs: Not yet synced
     → Sync now? (recommended)

You: Yes

AI:  ✓ Synced specs to openspec/specs/ui/spec.md
     ✓ Moved to openspec/changes/archive/2025-01-24-add-dark-mode/

     Change archived successfully.
```

---

## Snippet 5 · OpenSpec Project Structure Example

**来源**：<https://github.com/fission-ai/openspec/blob/main/openspec/specs/openspec-conventions/spec.md>

Illustrates the standard directory structure for an OpenSpec project, including locations for project context, agent instructions, specifications, and proposed changes.

```text
openspec/
├── project.md              # Project-specific context
├── AGENTS.md               # AI assistant instructions
├── specs/                  # Current deployed capabilities
│   └── [capability]/       # Single, focused capability
│       ├── spec.md         # WHAT and WHY
│       └── design.md       # HOW (optional, for established patterns)
└── changes/                # Proposed changes
    ├── [change-name]/      # Descriptive change identifier
    │   ├── proposal.md     # Why, what, and impact
    │   ├── tasks.md        # Implementation checklist
    │   ├── design.md       # Technical decisions (optional)
    │   └── specs/          # Complete future state
    │       └── [capability]/
    │           └── spec.md # Clean markdown (no diff syntax)
    └── archive/            # Completed changes
        └── YYYY-MM-DD-[name]/
```

---

## 关于本摘录

- 这是 Context7 返回的**部分摘录**，不是全文。完整内容以上游 GitHub 仓库为准。
- Context7 索引可能落后于上游 `main` 分支最新 commit；若需最新，重新查同一库 ID 即可。
- 本文件是 [../wiki/openspec.md](../wiki/openspec.md) 的原始证据层。wiki 页里所有对 OpenSpec 命令 / 工作流的描述都应能追溯回此文件某 snippet 或上游 URL。
- 本文件受 raw/ 只读约定保护——LLM 不修改或删除。需要刷新上游时，新建 `openspec-official-docs-excerpt-YYYY-MM-DD.md`，不覆盖本文件。
