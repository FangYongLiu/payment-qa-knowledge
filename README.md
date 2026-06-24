# payment-qa-knowledge

Payment QA 团队的**权威知识库** —— 唯一可信源。只存**经评审的** markdown / yaml 知识,
**不放代码**(代码在引擎仓 `payment-qa-brain`)。

知识引擎(`payment-qa-brain`)据本仓重建运行时索引(PostgreSQL + pgvector);
合并 PR 触发 reindex。

## 双层知识模型
- **底座 · LLM-Wiki 页(`wiki/`)** —— 每篇源文档 → 一篇带链接的 markdown 页(轻元数据
  `domain` + `tags` + `[[链接]]`)。灵活可读,容纳任何文档(业务概览、规格、笔记)。
- **上层 · 类型对象(`domains/`)** —— **仅技术内容**额外抽成 8 类对象 + 关系进图谱
  (撑需求影响分析 + 用例生成)。业务概览停在 wiki 页。

> 不要把每篇文档都硬塞进 8 类(那是 v1 的错)。业务级内容留作 wiki 页,类型对象只留给技术内容。

## 目录
- `domains/<域>/<file>.md` —— 类型知识对象(按 12 业务域分目录;**以服务为锚**,API/表/场景/自动化挂其上)
- `wiki/<域>/<slug>.md` —— LLM-Wiki 底座页(每篇源文档一页)
- `bimo-confirmed/<slug>.md` —— BimoQA 对话中确认、经 publish 发布的权威知识(按来源分桶,顶层独立目录)
- `templates/` —— 8 类对象模板 + **`README.md`(新建 / 上传文档前必读规范)**
- `index/domains.yaml` —— 12 业务域注册表(owner / reviewer 权威源 + 路由)
- `legacy/` —— 旧的零散内容(已隔离,不进检索;待重整理)

> 物理目录给人看;检索靠元数据 + 向量 + 图,不依赖目录结构。改文件名**不改 id**(reindex 按 id 重建)。

## 8 类对象
Domain / Service / API / Table / Flow / Scenario / Troubleshooting / AutomationAsset。
每个 = 一个 markdown + frontmatter 元数据。**编写规范(模板 + 全连边)见 [`templates/README.md`](templates/README.md)**。
完整样板见 `domains/kyc/`(Domain → Service → API → Scenario → Automation 五层全连边)。

## 怎么贡献
首选工作台 / 引擎的 update-request 流程(具名提交 → 评审 → 引擎开 PR)。评审 UI 里的
**批准是人审门**;引擎随后自动开并合并自己的 PR(方案 B),合并触发 reindex。
直接改本仓也走 PR + 评审。流程见 [`CONTRIBUTING.md`](CONTRIBUTING.md)。

## 校验
提交前 / CI 跑 `python scripts/check_knowledge.py`(引擎仓):确认 `related_*` 与 eval 引用无悬空 id。
