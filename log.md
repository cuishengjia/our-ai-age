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
