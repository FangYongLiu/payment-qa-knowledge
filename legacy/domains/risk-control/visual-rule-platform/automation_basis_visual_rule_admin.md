---
id: auto_basis_visual_rule_admin
object_type: AutomationAsset
domain: risk-control
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:00c6a300-c75b-4c5d-b0c9-c18e010dfb50
tags:
- admin-portal
- visual-rule
- strategy-manager
- list-manager
- cache-clear
subdomain: visual-rule-platform
module: null
sensitivity: normal
name: Basis 风控可视化规则管理后台
aliases:
- Basis Admin
- bigdata-admin
related_services: []
related_tables:
- bigdata_list_repo
- bigdata_system_dic
related_scenarios:
- risk-visual-rule-hierarchy
- risk-visual-rule-authoring-guide
- risk-visual-rule-activation-workflow
- risk-verifyrisk-firing-and-verification
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
Basis 风控可视化规则管理后台（Basis Admin，UAT 入口 `uat.intra.azure.test2pay.com/bigdata-admin/`）是风控运营管理界面，用于：

- 管理 Visual Rules / Group Rules / Strategy Set
- 维护 Strategy → Checkpoint → Rule 层级结构
- 维护 List 仓库（`bigdata_list_repo`）与系统字典（`bigdata_system_dic`）
- 执行运行时缓存清理（Function Query → Cache Clear）

## 使用方式
后台主要承载以下入口：

- **Visual Rule / Strategy / List Manager 页面**：
  - 创建 Strategy（folder、status、effective time）并绑定 Checkpoint（如 `FT Add to list`、`FT_ATL_CP`）
  - 在 Strategy 下创建 Visual Rule，配置条件（event 字段、比较、AND/OR 分组）
  - 配置 Action：`ADD_TO_LIST`、`REJECT`、`REVIEW`、`PASS`、value-set actions 等
  - 通过 Fields 下拉选择字段，受 `listRepoFieldType`（oneRow）或 `fieldDef` 列（mostRow）过滤
  - 保存为 `DRAFT`

- **激活流程**（在 Visual Rule UI 上推进状态机）：
  - `DRAFT` → 点击 TRIAL → 等待 ≥1 分钟（系统强制） → 点击 Enabled → 提交审核 → 由另一名操作员在 AstraShield 的 Audit Record 审批 → `ENABLED` → 等待约 35 秒缓存重载后生效
  - Trial-mode 短路在 Rule 层与 Strategy 层各自独立生效

- **Function Query → Cache Clear**：
  - 路径：Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → 执行 `systemParam` Clear + `ip` Clear

- **回滚路径**：
  - 通过 Visual Rule UI 直接 disable 规则；或翻转 `aml.t_system_param` 标志后再做 Cache Clear

## 关键配置
- **List 仓库 `bigdata_list_repo`**：
  - `listRepoAttr=oneRow` vs `mostRow`
  - `fieldDef` 列定义，最多 3 列
  - 典型仓库：`LAF_blocklist`、`LAF_appeal_acceptlist` 等
- **系统字典 `bigdata_system_dic`**：
  - `addListRepos`：合法 `repoNo` 白名单
  - `listRepoFieldType`：oneRow 字段类型字典
- **Strategy 版本控制**：同一 Strategy 只有一个 deployed 版本，非 deployed 版本下的规则不会对真实事件触发
- **Action 写库语义**：
  - `oneRow`：单 `[type, value]` 对，部分字段空值时静默跳过该 attr
  - `mostRow`：多列行，任一列空值则整行 abort
- **审计 memo 格式**：`'from visual rule, eventId=<id>'`，`eventId` 取自请求 header，非 body
- **未知 `repoNo`**：被 `addListRepos` 字典拒绝
- **被热删除的目标 list repo**：graceful no-op + 日志，不抛异常

## 注意事项
- **Strategy 版本陷阱**：规则挂在非 deployed 版本下不会生效，必须确认部署版本
- **Checkpoint 来源校验**：确认绑定的 Checkpoint 是真实 CGS event source 而非 test-only
- **字段名精确匹配**：payload 字段名必须与列字段名完全一致（区分大小写，无自动映射），EN/ZH tooltip 已强调
- **审批职权分离**：能否审批自己提交的规则因产品域而异；MLIMIT 类管控下互斥更严格
- **激活等待窗口**：约 1.5 分钟自身耗时 + 审计 + 35 秒缓存重载
- **Cache Clear 必要性**：仅在 Risk Param 页 Save 不足以让运行时生效，必须执行 `systemParam` + `ip` Clear
- **Kill Switch 非热更新**：需要 Tomcat 重启，重启后再验证
- **Trial-mode 规则**：仅写日志、不执行 action，验证方式是确认 list repo 无写入行
- **两层开关模型**：Apollo YAML（构建/重启时）+ `aml.t_system_param`（运行时，可缓存刷新）
