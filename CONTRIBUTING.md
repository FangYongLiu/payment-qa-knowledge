# 知识贡献与评审指南

面向全体 QA 成员。目标：让知识可信、可溯源、可治理。

## 1. 新建知识对象
1. 从 `templates/` 复制对应类型模板到 `domains/<domain>/<object_type>/`。
2. 命名遵循 id 约定：`api_<service>_<name>` / `svc_<name>` / `tbl_<schema>_<table>` / `scn_<name>` / `ts_<symptom>` / `auto_<name>` / `flow_<name>` / `domain_<slug>`。
3. 填写 frontmatter（必填字段不可缺），并在 `related_*` 写明关联对象的 id。
4. 在对应 `index/<type>.yaml` 增加路由项（id/name/aliases/domain/status/path）。

## 2. 元数据规范
- 必填：id, object_type, domain, subdomain, module, status, owner, reviewer, last_reviewed_at, source_type, source_ref, tags。
- 选填：name, aliases, related_services, related_tables, related_scenarios, related_logs, related_requirements, related_failures。
- status：draft（新建）→ active（评审通过）→ deprecated/archived。
- `name` + `aliases` 决定中英文问法能否命中，务必写全（如 "DCC"/"DCC资质"/"dcc qualification"）。

## 3. related_* 写法
- 只写**真实存在**的对象 id；不能悬空。
- 写"已知关系"（API→Service/Table/Scenario/Log）；推断型关系（failure→root_cause 等）由引擎在整理阶段产出、人审入库。

## 4. 评审要求
- 实名提交；由该域 Domain Owner / Reviewer 评审。
- 评审看：事实正确性、元数据完整、related_* 正确、status 合理。
- 通过后才置 active；只有 active 进生产回答。

## 5. 提交前检查
- 跑引擎仓库的 `scripts/check_knowledge.py`：related_* 与 eval 的 expected_object_ids 无悬空。
- 一个对象一个文件；改动走 PR。
