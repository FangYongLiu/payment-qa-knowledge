---
id: flow_mpgs_manual_onboarding
object_type: Flow
domain: merchant-acquisition-testing
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/684425357
tags:
- MPGS
- manual-onboarding
- flow
subdomain: onboarding
module: null
sensitivity: normal
name: MPGS手动报备端到端流程
aliases: []
related_services: []
related_tables:
- tbl_onboarding_t_fund_provider
- tbl_onboarding_t_manual_register_rule
- tbl_onboarding_t_manual_register_rule_field
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
针对MPGS E-com快速上线场景，商户在外部供应商(MPGS Onboarding Portal 线下)完成报备后，通过Payby的手动录入入口将商户、门店、设备登记信息回传写入Payby系统。流程涉及 onboarding 服务(报备规则管理、手动报备信息入口)与 basis 服务(配置登记类型、登记页面人工录入)。

## 步骤(跨系统)
1. 供应商配置阶段(basis 服务页面)：
   - 在 FundProvider 配置中选择登记类型(SYSTEM_AUTO 或 MANUAL)，本次新增 MANUAL(人工录入)。
   - 配置人工录入的登记规则与字段(写入 t_manual_register_rule、t_manual_register_rule_field)。
2. 配置查询：
   - 调用 getConfig 接口，返回 registerType 标识供应商登记类型；若 registerType=Manual 则 onboardingRuleList 为空。
3. 商户线下报备：商户在外部供应商(MPGS Onboarding Portal)完成注册。
4. 人工录入入口(Onboarding Management 页面)：
   - 展示 edit sync 入口，弹出人工录入弹窗(展示UI流程 + 提交流程)。
   - 录入商户、门店、设备信息后提交。
5. 手动报备数据写入(onboarding 服务，方案三)：
   - 调用 manualRegister 接口。
   - 接口内部将录入数据转换为登记 item 与 item_result_map 数据进行存储，并设置为激活状态。
   - 若上报数据字段中 key 已存在对应数据则进行覆盖。
   - 写入失败则直接抛错由上游重试。
6. 结果展示：FundProvider Query 页面展示人工录入结果，状态为激活。

## 涉及服务/表
- 服务：
  - onboarding：报备规则管理模块(新增登记类型配置)、新增手动报备信息入口(manualRegister)。
  - basis：页面支持配置登记类型、登记页面支持人工录入信息进行报备。
- 表：
  - [[tbl_onboarding_t_fund_provider]]：新增 register_type 字段(SYSTEM_AUTO、MANUAL)。
  - [[tbl_onboarding_t_manual_register_rule]]：人工登记规则表。
  - [[tbl_onboarding_t_manual_register_rule_field]]：人工登记字段配置表。
- 接口：
  - [[api_onboarding_get_config]]：返回 registerType；MANUAL 时 onboardingRuleList 为空。
  - [[api_onboarding_manual_register]]：人工录入数据转换为 item、item_result_map 写入。

## 校验点
- getConfig 返回的 registerType 与供应商配置一致；当 registerType=Manual 时 onboardingRuleList 为空。
- 人工录入提交后，item 与 item_result_map 数据写入成功且状态为激活。
- 上报数据字段中 key 若已存在，新值应覆盖旧值。
- 写入失败时接口抛错，支持上游重试。
- 自动报备流程不处理 MANUAL 类型(自动与手动逻辑隔离，方案三不依赖 OnboardingOrder)。
- FundProvider Query 页面可查看到人工录入结果，状态为激活。
