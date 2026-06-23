# 知识贡献与评审指南

面向全体 QA。目标:可信、可溯、可治理的知识。

> **怎么写每类文档(模板 / frontmatter / 关联关系 / 全连边回写)见 [`templates/README.md`](templates/README.md)。
> 本文只讲分流、元数据要点与评审流程,不重复编写细节。**

## 1. 内容放哪(双层分流)
- **业务概览 / 混合文档** → `wiki/<域>/` 下的 LLM-Wiki 页(通常引擎据源文档自动生成)。
- **技术内容**(API / 表 / 场景 / 排障 / 自动化)→ `domains/<域>/` 下的类型对象。
- **BimoQA 对话中确认、经 publish 发布的权威知识** → **`wiki/bimo-confirmed/`**
  (`domain: bimo-confirmed`,`source_type: conversation`)。按**来源**单独分桶,目录名一眼可见
  这些是"对话确认"来的;文件 slug 用描述性前缀(如 `kb-conventions-owner-field`)。

## 2. 元数据规范要点
- **必填**:`id`、`object_type`、`domain`、`status`、`owner`、`reviewer`、`last_reviewed_at`、`source_type`、`source_ref`、`tags`。
- **owner / reviewer = 知识负责人**,按 `index/domains.yaml` 的 12 域映射填(**≠ `dev_owner` 开发联系人**)。
- **可选**:`name`、`aliases`、`app_group` / `layer` / `dev_owner`(服务专有)、`related_*`。
- `status`:服务骨架默认 `active`(零认领即有服务全景);评审流程新建的内容 `draft` → `active`(评审通过)。只有 `active` 进生产检索。
- `name` 必须人类可读;代码名 / 部署名放 `aliases`(中英文俗称都列,影响检索命中,如 `DCC` / `dcc 资质`)。

## 3. related_* / 连边
- 只引用**真实存在**的对象 id —— **无悬空**(对象还没建就在正文写名字 + 标「待补」,别硬连)。
- 只声明**已知**关系;边只从自然源头声明一次(单边声明 + 边归属矩阵见 `templates/README.md` §3)。
- 推断关系(故障 → 根因等)由引擎 curation 产出,人审后才进图。

## 4. 评审(人审门)
- 具名提交;由该域 Owner / Reviewer 评审。
- 评审看:事实正确、元数据齐全、`related_*` 正确无悬空、`status` 合理。
- **批准 = 人审门(方案 B)**:引擎随后自动开并合并自己的 PR + reindex。

## 5. 提交前检查
- 跑 `scripts/check_knowledge.py`(引擎仓):`related_*` 与 eval 的 `expected_object_ids` 无悬空。
- 一个对象一个文件;所有改动走 PR。
- **新增对象务必回写相关文档的关联**(全连边,见 `templates/README.md` §4)。
