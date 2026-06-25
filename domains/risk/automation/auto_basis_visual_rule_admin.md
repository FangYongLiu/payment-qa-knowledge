---
id: auto_basis_visual_rule_admin
object_type: AutomationAsset
name: Basis 风控可视化规则管理后台
aliases:
- Basis Admin
- bigdata-admin
- PAYBY BASIS
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2161541121
tags:
- admin-portal
- visual-rule
- strategy-manager
- list-manager
- cache-clear
related_scenarios:
- scn_grc_config_effectiveness
- scn_grc_identity_3ds_rule
related_services:
- svc_grc_component_connect_provider
- svc_bigdata_admin
- svc_grc_check_identity_provider
---

# Basis 风控可视化规则管理后台

## 用途
Basis 风控可视化规则管理后台(Basis Admin / PAYBY BASIS,UAT 入口 `uat.intra.azure.test2pay.com/bigdata-admin/`,另有 `sim.intra.test2pay.com/basis/`)是风控运营管理界面,用于:管理 Visual Rules / Group Rules / Strategy Set;维护 Strategy → Checkpoint → Rule 层级;维护 List 仓库(`bigdata_list_repo`)与系统字典(`bigdata_system_dic`);维护核身规则(Identity Rule);执行运行时缓存清理(Function Query → Cache Clear);承载 General Audit 审核记录。其承载的核心服务为 [[svc_bigdata_admin]],对接风控引擎 [[svc_grc_component_connect_provider]] 与核身服务 [[svc_grc_check_identity_provider]]。

## 关联关系
- **覆盖的场景**:[[scn_grc_config_effectiveness]]、[[scn_grc_identity_3ds_rule]](= `related_scenarios`)
- **针对/跑在的服务**:[[svc_bigdata_admin]]、[[svc_grc_component_connect_provider]]、[[svc_grc_check_identity_provider]](= `related_services`)
- **触发的接口**:[[api_grc_verify_risk]];排障见 [[ts_risk_rule_not_firing]]

## 使用方式
### Strategy → Checkpoint → Rule 三层
- **Strategy**:顶层容器,具 folder、status、effective time;有版本概念,**同一策略仅一个版本被部署生效**,挂在非 deployed 版本下的规则永不在真实事件触发。参考测试策略 `FT_PAYM2755_TEST`。
- **Checkpoint**:策略绑定到具体业务事件源的接入点(如 `FT Add to list`、`FT_ATL_CP`);需确认是真实 CGS 事件源而非 test-only。
- **Rule**:最小执行单元,含条件(event 字段、比较、AND/OR 分组)与 Action。

### Action 类型
`ADD_TO_LIST`(写入 List Repo)、`REJECT`、`REVIEW`、`PASS`、value-set actions 等。`ADD_TO_LIST` 写入形态由目标 List Repo 的 `listRepoAttr` 决定。

### 激活流程(状态机,系统强制顺序)
`DRAFT` → 点 TRIAL → 等待 ≥1 分钟 → 点 Enabled(提交审核)→ 另一名操作员在 AstraShield Audit Record 审批 → `ENABLED` → 等 ~35s 缓存重载 → 生效。预期窗口:~1.5 min 自计时 + 审批人 + 35s 缓存重载。审批通过产出 Audit Record(可截图留档)。

### 缓存清理(Function Query → Cache Clear)
GENERAL → Function Query → Cache Clear,搜索 `grc` 返回 4 个服务:`gp079_grc-component-connect-provider`(Action 含 `caffeineCacheManager`、`cacheManager`)、`gp079_grc-cps-provider`、`gp079_grc-engine-provider`、`gp079_grc-check-identity-provider`。运行时参数生效:选 `gp079_grc-component-connect-provider` → `systemParam` Clear + `ip` Clear(见 [[scn_grc_config_effectiveness]])。

### 核身规则与审核
RISK CONTROL → Risk Event → Identity Rule Management 维护核身规则(EventType / Rules / IdentityType / Priority,见 [[scn_grc_identity_3ds_rule]]);新增/生效/停用经 GENERAL → General Audit → Audit Record 审核(`AuditType = GRC_IDENTITY_RULE`、`Abbreviation = Update Identity Rule`,`AuditStatus` WAITING → 通过)。

## 关键配置
- **List 仓库 `bigdata_list_repo`**:`listRepoAttr=oneRow`(单 `[type,value]` 对,字段下拉由 `listRepoFieldType` 过滤,部分空值静默跳过该 attr)vs `mostRow`(多列行,列由 `fieldDef` 定义、最多 3 列,字段下拉由 `fieldDef` 过滤,任一列空值整行 abort)。典型仓库:`LAF_blocklist`、`LAF_appeal_acceptlist`。
- **系统字典 `bigdata_system_dic`**:`addListRepos`(合法 `repoNo` 白名单,未知 repoNo 被拒)、`listRepoFieldType`(oneRow 字段类型字典)。
- **字段名精确匹配**:payload 字段名必须与列字段名完全一致(区分大小写,无自动映射,EN/ZH tooltip 已强调)。
- **审计 memo 格式**:`'from visual rule, eventId=<id>'`,`eventId` 取自请求 Header 非 body。
- **被热删除的目标 list repo**:graceful no-op + 日志,不抛异常。

## 注意事项
- **Strategy 版本陷阱**:规则挂在非 deployed 版本下不生效,必须确认部署版本。
- **Trial-mode 短路**:rule-level 与 strategy-level 各自独立;trial 仅写日志不执行 action,验证靠 list repo 无写入行。
- **Kill Switch 非热更新**:Apollo YAML 类需 Tomcat 重启后再验证。
- **审批职权分离(SoD)**:能否审批自己提交的规则因产品域而异,MLIMIT 类管控更严格。
- **Checkpoint 来源校验**:确认绑定的是真实 CGS event source 而非 test-only。
- 规则不触发时的完整自查见 [[ts_risk_rule_not_firing]]。
