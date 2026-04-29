# wiki/

**LLM 维护的结构化条目层。**

## 页面类型（`type` 字段）

| type | 用途 | 例 |
|---|---|---|
| `concept` | 方法、框架、模式 | `openspec.md` |
| `entity` | 产品、公司、人、工具 | `claude-code.md` |
| `synthesis` | 跨条目对比、地图 | `agent-tools-对比.md` |
| `observation` | 用户的判断、预测（明确观点） | `2026-ai-pm-差别.md` |

## Frontmatter

每个 wiki 页顶部必备 YAML：`title` / `type` / `tags[]` / `created` / `updated` / `sources[]` / `status`。

## 角色

- **用户**：读、评论、校对关键判断。
- **LLM**：写、维护、交叉引用、lint。

---

完整规范见 [../CLAUDE.md](../CLAUDE.md)。
