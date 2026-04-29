# Our AI Age — Log

时间轴，append-only。格式：`## [YYYY-MM-DD] <op> | <subject>`

查最近：`grep "^## \[" log.md | tail`

---

## [2026-04-29] setup | 初始化仓库
- `git init` + 公开 GitHub repo <https://github.com/cuishengjia/our-ai-age>
- 首次 commit `8ca8e14`（main 分支）：`README.md` + `.gitignore`
- Author 邮箱 `cuishengjia@live.cn`（repo-local，覆盖全局 `@xiaomi.com`）

## [2026-04-29] setup | 接入 llm-wiki 方法论 + 搭脚手架
- 接入方法论原文 [llm-wiki.md](./llm-wiki.md)
- 新建 [CLAUDE.md](./CLAUDE.md)（工作规约 schema）
- 新建 [index.md](./index.md)（wiki 目录）
- 新建 [log.md](./log.md)（本文件）
- 新建 [raw/](./raw/) + [wiki/](./wiki/) 两层目录（各附 README）

## [2026-04-29] ingest | OpenSpec 官方文档（via Context7 MCP）
- 源：<https://github.com/fission-ai/openspec>（Context7 库 ID `/fission-ai/openspec`，Medium reputation / benchmark 75.8）
- 新建 [raw/openspec-official-docs-excerpt.md](./raw/openspec-official-docs-excerpt.md)——5 个 snippet，完整 provenance
- 新建 [wiki/openspec.md](./wiki/openspec.md)（concept 页）——PM 视角 4 步 playbook + review 清单 + 起手 checklist + 待填区
- 更新 [index.md](./index.md)——概念页区加 OpenSpec 条目
- 规则新增：README 是仓库导航页，每次 ingest 跟随更新（用户 2026-04-29 确立）
- 同 commit 更新 [CLAUDE.md](./CLAUDE.md) Ingest 流程（加"更新 README 导航"步）
- 同 commit 更新 [README.md](./README.md) 加导航区 + 最近条目 + 仓库结构
- 保存 feedback memory：(1) always register source provenance；(2) README-as-navigation
