# Our AI Age

一名 AI 产品经理的公开笔记本。

这里记录我在 AI 领域工作和学习的心得——
从模型能力到产品落地，
从用户洞察到行业观察，
写得最多的，是一线 PM 视角下
「能用、好用、值得用」的判断。

如果你也是 AI 产品的从业者、学习者，
或者只是对这个时代好奇，欢迎一起看。

持续更新中。

---

## 浏览

- **[Wiki 目录](./index.md)** — 按类型索引所有条目
- **[Log 时间轴](./log.md)** — 最近做了什么、什么时候做的
- **[方法论](./llm-wiki.md)** — 这个仓库怎么运作（LLM-wiki 模式）
- **[工作规约](./CLAUDE.md)** — LLM 在这里的操作手册

## 最近的条目

### 概念

- **[OpenSpec](./wiki/openspec.md)** — spec-driven AI coding 工作流；PM 视角 4 步 playbook（propose → review → apply → archive），存量项目加 feature 的对齐利器

_条目还不多，会持续长出来。_

## 仓库结构

```
.
├── README.md         # 你在这里——导航页
├── index.md          # 按类型索引的 wiki 目录
├── log.md            # 时间轴（append-only）
├── raw/              # 原始源材料（immutable，LLM 只读）
├── wiki/             # 结构化条目（concept / entity / synthesis / observation）
├── CLAUDE.md         # 工作规约（LLM 用）
└── llm-wiki.md       # 方法论原文
```

---

仓库按 **LLM-wiki 模式**运作：我 curate 源、提问、判断；LLM 做 bookkeeping——读源、写条目、维护交叉引用、定期 lint。方法论原文见 [llm-wiki.md](./llm-wiki.md)。
