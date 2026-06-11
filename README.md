# payment-qa-knowledge

Payment QA 团队的**正式知识仓库**——唯一可信源（single source of truth）。
只存**已评审**的 markdown/yaml 知识内容；**不存代码**（代码在 payment-qa-knowledge-brain）。

知识引擎从本仓库派生运行时索引（PostgreSQL+pgvector），合并 PR 后触发 reindex。

## 目录
- `domains/<domain>/<object_type>/` — 按业务域组织的知识对象（主组织方式）
- `templates/` — 8 类对象模板（新建对象从这里复制）
- `index/` — 各对象类型的路由索引（id/name/aliases/domain/status/path）
- 跨域共用对象才放顶层 `services/ apis/ database/`

> 物理目录主要给人看；检索靠 index/ + 元数据 + 向量，不依赖目录布局。

## 知识对象（8 类）
Domain / Service / API / Table / Flow / Scenario / Troubleshooting / AutomationAsset。
每个对象 = 一个 markdown 文件 + frontmatter 元数据。元数据规范见 CONTRIBUTING.md。

## 贡献方式
**优先**通过工作台/知识引擎的更新请求工作流（实名 → 评审 → 自动开 PR）。
直接改本仓库也需走 PR + 评审。详见 CONTRIBUTING.md。

## 校验
提交前/CI 跑 `python scripts/check_knowledge.py`（在引擎仓库），确保 related_* 与 eval 引用无悬空。
