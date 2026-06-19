---
title: 风控QA第一周入职培训计划(Foundation & Access)
domain: risk-control
kind: wiki_page
slug: risk-qa-week1-onboarding-plan
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2161541121
tags: []
---

# 风控QA第一周入职培训计划(Foundation & Access)

第一周入职培训覆盖 Day1–Day5，从账号权限开通到风控系统基础、Visual Rule 创作、规则激活与触发验证，最后在 Day5 进行端到端实操考核。培训目标是让新成员掌握 Risk System 规则全生命周期与验证流程，并能在升级问题之前独立完成基础排查。

## 总体目标(Objectives)

- 完成所有 QA 必需账号与访问权限的开通
- 理解商户支付业务的基本流程
- 熟悉相关数据库查询
- 掌握基础测试与问题排查能力

## Day 1｜Team Introduce & Account Permission

聚焦团队介绍与所有必要账号权限的开通。详细清单见 [[risk-qa-account-access-checklist]]。

待开通项目：
- **IPA Account** — `https://ipa1.corp.algento.com/ipa/ui/`，使用企业域账号修改密码
- **VPN Access** — VPN 地址 `20.74.221.9:443`
- **JIRA Account** — `https://algento.atlassian.net/jira/your-work`，使用 AstraTech 邮箱登录，可访问 PAYM-2755
- **Wiki Account** — `https://algento.atlassian.net/wiki/home`，可访问 AQ 空间
- **CI/CD Platform** — `https://appcenter-new.corp.payby.com/#/index`
- **BMOC Portal Access** — SIM `https://sim-admin.corp.test2pay.com/bmoc/`、UAT `https://uat-admin.corp.test2pay.com/bmoc/`
- **GitLab Access** — `https://gitlab.test2pay.com/qa/cgs-apitest`

**Passing Criteria**
- 无账号阻塞问题
- 知道账号异常如何处理

## Day 2｜Risk System Foundations & Visual Rule Overview

熟悉风控系统架构与 Visual Rule UI，详见 [[risk-system-architecture-overview]]。

**Risk Architecture 学习项**
- 理解 GRC 组件 `gp079_grc-component-connect-provider` 在请求路径中的角色
- 理解事件类型 `PAYMENT`、`ENTER_WALLET`、`CASHDESK_INIT` 与身份事件，及其分别落入 `grc.t_payment_event_<yyyy>` 还是 `grc.t_other_event_<yyyy>`
- 理解双开关模型：Apollo YAML(构建/重启时)+ `aml.t_system_param`(运行时、可缓存刷新)
- 理解 IP-area resolver(legacy `Ip2location` vs MaxMind GeoIP MMDB) 与路径接入签名 `remoteIpInfo._id`

**Visual Rule UI Tour 学习项**
- Visual Rules vs Group Rules vs Strategy Set
- Strategy → Checkpoint → Rule 层级
- Action 类型：`ADD_TO_LIST`、`REJECT`、`REVIEW`、`PASS`、value-set actions 等
- List 仓库 `bigdata_list_repo`：`listRepoAttr=oneRow` vs `mostRow`、`fieldDef` 列、3 列上限
- 系统字典 `bigdata_system_dic`：`addListRepos`、`listRepoFieldType`

**Expected Outcome**
- 已开通 Basis Admin(`uat.intra.azure.test2pay.com/bigdata-admin/`)、AstraShield、Kibana、MongoDB(`grc`/`aml`/`bigdata`)只读权限
- 能说出某事件类型写入哪个 DB collection
- 能列出 3+ 个活动 strategy 及其绑定 checkpoint
- 能说明 oneRow vs mostRow 列语义

**Evaluation Gate**：口头还原一次 [[api_grc_verify_risk]] 请求从 API 入口到事件文档持久化的完整路径；在 UAT 上展示一个 oneRow 与一个 mostRow 仓库并解释列模式。

## Day 3｜Visual Rule Authoring

实操创作 Visual Rule，详见 [[risk-visual-rule-authoring-guide]]。

**Strategy & Checkpoint**
- 创建测试 strategy(folder、status、effective time)
- 绑定到 checkpoint(如 `FT Add to list`、`FT_ATL_CP`)
- 理解 strategy 版本陷阱：只有一个版本会被部署，未部署版本下的规则无法对真实事件生效
- 确认 checkpoint 接的是真实 CGS 事件源，而非 test-only
- 参考已有测试 strategy `FT_PAYM2755_TEST`

**Rule Authoring**
- 在自己的 strategy 下创建 Visual Rule
- 配置条件(事件字段、比较、AND/OR 组)
- 配置 `ADD_TO_LIST` action：`oneRow`(单个 `[type,value]` 对) 与 `mostRow`(多列行) 两种模式
- Fields 下拉按 `listRepoFieldType`(oneRow) 或 `fieldDef` 列(mostRow) 过滤
- EN/ZH tooltip：payload 字段名必须与列字段名完全匹配(大小写敏感、无自动映射)
- 保存为 `DRAFT`

**Expected Outcome**
- 至少各创作一条 `oneRow` 与 `mostRow` 规则(DRAFT 状态)
- 为每条规则选对目标 list repo(如 `LAF_blocklist`、`LAF_appeal_acceptlist`)
- 能口头解释 Strategy → Checkpoint → Rule 层级
- 能从零起草带两种 action 变体的 Visual Rule

## Day 4｜Rule Activation, Firing & Verification

覆盖规则激活流程、事件触发与验证、缓存与 Kill Switch。

### Activation Workflow

详见 [[risk-visual-rule-activation-workflow]]。

- 完整状态机：`DRAFT → 点 TRIAL → 等待 ≥1 分钟(系统强制) → 点 Enabled → 提交审核 → 由另一名操作员在 AstraShield Audit Record 审批 → ENABLED → 等 ~35s 缓存重载 → 生效`
- 职责分离(SoD)：能否审批自己提交的规则因产品域而异；MLIMIT 类管控更严
- Trial-mode 短路在 rule-level 与 strategy-level 各自独立生效
- **Evaluation Gate**：将一条规则端到端从 `DRAFT` 推到 `ENABLED`，并产出 Audit Record 截图；知道预期等待窗口(~1.5 min 自身 + auditor + 35s 缓存重载)

### Firing Events

详见 [[risk-rule-firing-and-verification]]。

- Endpoint：`https://uat-api-intra.test2pay.com/newriskverify`
- Payload：[[api_grc_verify_risk]] 请求，`eventBody` 携带规则条件/列所用字段
- 字段名精确匹配契约(无自动映射)
- `eventId` header → 审计 memo `'from visual rule, eventId=<id
