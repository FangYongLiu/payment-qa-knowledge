---
id: tbl_onboarding_t_fund_provider
object_type: Table
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/684425357
tags:
- onboarding
- fund_provider
- register_type
subdomain: onboarding
module: fund_provider
sensitivity: normal
name: 资金供应商配置表 t_fund_provider
aliases: []
related_services:
- svc_onboarding
---

## 用途
资金供应商配置表，用于配置 onboarding 资金供应商相关信息。本次 MPGS 手动报备改造在该表上新增 `register_type` 字段，用于标识供应商的登记类型(系统自动 / 人工录入)，以便 onboarding 服务的报备规则管理模块据此分流处理逻辑。

## 关键列
- `register_type` varchar(50) NOT NULL DEFAULT 'SYSTEM_AUTO'
  - 含义：报备类型
  - 取值：
    - `SYSTEM_AUTO`：系统自动报备(默认值)
    - `MANUAL`：人工录入报备
  - 影响：当 `register_type=MANUAL` 时，`getConfig` 接口返回的 `onboardingRuleList` 为空(改由人工登记规则表 `t_manual_register_rule` / `t_manual_register_rule_field` 提供配置)

## 主键/索引
本次变更仅新增字段，未涉及主键或索引调整(原文未给出主键/索引定义)。

DDL：
```sql
ALTER TABLE `onboarding`.`t_fund_provider`
ADD COLUMN `register_type` varchar(50) NOT NULL DEFAULT 'SYSTEM_AUTO' COMMENT '报备类型，SYSTEM_AUTO、MANUAL'
```

## 校验点(QA 关注)
- 新增 `register_type` 字段对存量数据：默认值 `SYSTEM_AUTO`，存量供应商行为应保持自动报备不变。
- `register_type` 仅允许 `SYSTEM_AUTO` / `MANUAL` 两种值；NOT NULL 不可为空。
- 配置页面(basis 服务)需支持选择 `register_type`，写库后被 onboarding 服务正确读取。
- `getConfig` 接口返回字段 `registerType`：
  - 值为 `MANUAL` 时，`onboardingRuleList` 必须为空。
  - 值为 `SYSTEM_AUTO` 时，按原有规则返回 `onboardingRuleList`。
- 切换登记类型(SYSTEM_AUTO ↔ MANUAL)时，需验证报备规则管理模块的分流逻辑(自动报备流程仅处理 `SYSTEM_AUTO`，`MANUAL` 走 `manualRegister` 接口)是否正确隔离，互不影响。
