# CLAUDE.md — payment-qa-knowledge(知识内容仓)

> 本仓只放**经评审的知识内容 —— 无代码**,是知识引擎(`payment-qa-brain`)的唯一可信源。

## 规则
- 只增改 markdown 知识(wiki 页 + 类型对象)+ `index/domains.yaml` 路由 —— **绝不放应用代码**。
- **双层模型**:每篇源 → 一篇 `wiki/` 页;**技术内容额外**在 `domains/` 下抽类型对象。
  别把每篇文档都硬塞进 8 类。
- 每个类型对象 = 一个 markdown + frontmatter;**编写规范见 [`templates/README.md`](templates/README.md)**
  (命名、frontmatter、关联关系段、全连边回写)。`name` 人类可读,代码名进 `aliases`。
- `related_*` 必须指向**真实存在**的对象 id —— **无悬空**。**新增对象时,回写所有相关对象的关联**
  (`templates/README.md` §4 的回写清单)。
- `status`:服务骨架默认 `active`;评审流程新建内容 `draft`,人审通过才 `active`。只有 `active` 进生产检索。
- 改文件名**不改 id**(reindex 按 id 重建,改名透明)。
- 所有改动走 PR。评审 UI 的批准是人审门;引擎自动开并合并自己的 PR(方案 B),合并即 reindex。
- 提交前跑 `scripts/check_knowledge.py`(引擎仓)确认无悬空 id。
