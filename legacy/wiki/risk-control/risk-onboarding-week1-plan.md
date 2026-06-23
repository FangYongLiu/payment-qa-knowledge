---
title: Risk System 新人Week1入职培训计划
domain: risk-control
kind: wiki_page
slug: risk-onboarding-week1-plan
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:00c6a300-c75b-4c5d-b0c9-c18e010dfb50
tags: []
---

# Risk System 新人Week1入职培训计划

风控QA新人第一周入职培训计划，覆盖账号开通、风控架构与 Visual Rule 体系学习、规则编写与激活、verifyRisk 事件触发与验证，以及第五天的综合考核。

## 培训目标

- 完成所有 QA 必需账号与权限开通
- 理解商户支付业务基础
- 熟悉相关数据库查询方式
- 掌握基础测试与问题排查能力

## Day 1 | 团队介绍 & 账号权限

主题：与 QA / Dev / Product / PMO 团队成员认识，并完成所有基础账号开通。

涵盖的账号与系统：

- IPA Account（`https://ipa1.corp.algento.com/ipa/ui/`，使用企业域账号改密）
- VPN Access（`20.74.221.9:443`）
- JIRA Account（`https://algento.atlassian.net/jira/your-work`，AstraTech 邮箱登录；可访问 `PAYM-2755`）
- Wiki Account（`https://algento.atlassian.net/wiki/home`，可访问空间 `AQ`）
- CI/CD Platform（`https://appcenter-new.corp.payby.com/#/index`，域账号登录）
- BMOC Portal：SIM `https://sim-admin.corp.test2pay.com/bmoc/`，UAT `https://uat-admin.corp.test2pay.com/bmoc/`
- GitLab Access（`https://gitlab.test2pay.com/qa/cgs-apitest`）

对接人：QA `ext_Nitesh.Parasher@astratech.ae`、Ops `zhiqi.jin@astratech.ae`、PMO `Bilal.Javed@astratech.ae`、DBA `Li.Zhang@astratech.ae`。

考核标准：
- 无账号阻塞问题
- 知道账号异常时如何处理

详细清单见 [[risk-onboarding-account-access]]。

## Day 2 | 风控系统基础 & Visual Rule 概览

### Risk Architecture

学习要点：

- 理解 GRC 组件 `gp079_grc-component-connect-provider` 在请求链路中的角色
- 理解事件类型（`PAYMENT`、`ENTER_WALLET`、`CASHDESK_INIT`、identity events），及其落表归属：`grc.t_payment_event_<yyyy>` vs `grc.t_other_event_<yyyy>`
- 理解双开关模型：Apollo YAML（构建/重启时生效）+ `aml.t_system_param`（运行时，可通过缓存刷新）
- 理解 IP 区域解析器：legacy `Ip2location` vs MaxMind GeoIP MMDB；通过 `remoteIpInfo._id` 形态判断走哪条链路

参考：GRC architecture deck、PAYM-2744 IP-Location Optimization spec、bigdata-admin UI map。

考核：
- 已开通 Basis Admin（`uat.intra.azure.test2pay.com/bigdata-admin/`）、AstraShield、Kibana、`grc` / `aml` / `bigdata` MongoDB 只读权限
- 能说出某事件类型对应的落库 collection
- 口述一次 `verifyRisk` 请求从 API 入口到事件文档持久化的完整路径

### Visual Rule UI Tour

学习要点：

- Basis 上 Visual Rules vs Group Rules vs Strategy Set 的区别
- Strategy → Checkpoint → Rule 三层结构
- Action 类型：`ADD_TO_LIST`、`REJECT`、`REVIEW`、`PASS`、value-set actions 等
- List repos（`bigdata_list_repo`）：`listRepoAttr=oneRow` vs `mostRow`、`fieldDef` 列、3 列上限
- System dictionaries（`bigdata_system_dic`）：`addListRepos`、`listRepoFieldType`

考核：
- 能列出 3 个以上启用中的 strategy 及绑定的 checkpoint
- 能说明 `oneRow` vs `mostRow` 的列语义
- 在 UAT 上各演示一个 `oneRow` 与 `mostRow` 的 list repo

延伸阅读：[[risk-system-architecture-overview]]、[[risk-visual-rule-hierarchy]]、[[auto_basis_visual_rule_admin]]。

## Day 3 | Visual Rule 编写

### Strategy & Checkpoint

- 创建一个测试 strategy（folder、status、生效时间）
- 绑定到一个 checkpoint（如 `FT Add to list`、`FT_ATL_CP`）
- 注意 strategy 多版本陷阱：仅 ONE 个版本会被部署，挂在未部署版本下的规则不会在真实事件上触发
- 确认 checkpoint 接的是真实 CGS 事件源，而非 test-only
- 参考既有测试 strategy `FT_PAYM2755_TEST`

考核：
- 自己创建一个测试 strategy 并绑定到真实 checkpoint
- 能识别多版本 strategy 中 deployed 的那一份
- 演示自己创建的 strategy，并解释它能否在真实事件上触发

### Rule Authoring

- 在自己的 strategy 下新增一条 Visual Rule
- 配置条件（事件字段、比较、AND/OR 分组）
- 配置 `ADD_TO_LIST` action：分别用 `oneRow`（单 `[type,value]` 对）和 `mostRow`（多列行）两种模式
- Fields 下拉受 `listRepoFieldType`（oneRow）或 `fieldDef` 列（mostRow）过滤
- 注意 EN/ZH 提示：payload 字段名必须严格匹配列字段名（区分大小写、不会自动映射）
- 保存为 `DRAFT`

参考 list repo：`LAF_blocklist`、`LAF_appeal_acceptlist` 等。

考核：
- 至少在 `DRAFT` 状态完成 1 条 `oneRow` 规则 + 1 条 `mostRow` 规则
- 能为每条规则选对目标 list repo
- 独立完成全过程，并能基于 repo 的 `fieldDef` 解释列选择的合理性

Day 3 期望产出：能口述 Strategy → Checkpoint → Rule 层级；能从零起草两种 action 形态的 Visual Rule。

详见 [[risk-visual-rule-authoring-guide]]。

## Day 4 | 规则激活、触发与验证

### Activation Workflow

- 完整状态机：`DRAFT` → 点击 TRIAL → 等待 ≥1 分钟（系统强制）→ 点击 Enabled → 提交审核 → 另一名操作员在 AstraShield 的 Audit Record 审批 → `ENABLED` → 等待约 35 秒缓存刷新 → 真正生效
- 职责隔离：能否审批自己提交的规则因产品域而异；MLIMIT 类管控下互斥更严格
- Trial-mode 短路在 rule 级和 strategy 级各自独立生效

考核：
- 把一条规则从 `DRAFT` 走到 `ENABLED`
- 知道预期等待窗
