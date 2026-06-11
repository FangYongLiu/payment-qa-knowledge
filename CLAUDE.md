# CLAUDE.md — payment-qa-knowledge（知识内容仓库）

> 本仓库**只存已评审的知识内容，不存代码**。是知识引擎的唯一可信源。

## 规则
- 只新增/修改 markdown 知识对象与 index/ 路由，不写应用代码。
- 每个对象 = 一个 markdown + frontmatter；遵循 CONTRIBUTING.md 的元数据与命名规范。
- `related_*` 只指向真实存在的 object id，禁止悬空；新建对象要同步更新 index/<type>.yaml。
- status 默认 draft；只有人评审通过才置 active。
- 改动走 PR；不直接"发布"。

## 参考
- README.md：仓库结构与定位
- CONTRIBUTING.md：新建/评审/元数据规范
- templates/：8 类模板
- domains/online-business/acquire/：DCC 已填示例（可作参考范本）
