---
id: scn_onboarding_manual_register
object_type: Scenario
name: MPGS 供应商人工录入报备
aliases: [manual register, 人工报备, MANUAL onboarding]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/684425357
tags: [onboarding, mpgs, manual-register]
related_services: [svc_onboarding, svc_basis]
related_tables: [tbl_onboarding_t_fund_provider, tbl_onboarding_t_manual_register_rule, tbl_onboarding_t_manual_register_rule_field]
related_logs: []
---

# MPGS 供应商人工录入报备

## 触发 / 入口
- basis 门户 FundProvider 配置页:把供应商「登记类型」设为 `MANUAL`。
- basis 登记页人工录入弹窗 → 提交 → 调 [[api_onboarding_manual_register]];渲染前先调 [[api_onboarding_get_config]] 取人工登记规则。
- 完整端到端流程见 [[flow_mpgs_manual_onboarding]]。

## 关联关系
- **涉及服务**:[[svc_onboarding]] / [[svc_basis]](= `related_services`)
- **校验的表**:[[tbl_onboarding_t_fund_provider]] / [[tbl_onboarding_t_manual_register_rule]] / [[tbl_onboarding_t_manual_register_rule_field]](= `related_tables`)
- **相关日志**:`service:onboarding`(待补具体关键字)
- **测它的接口**:[[api_onboarding_manual_register]] / [[api_onboarding_get_config]](由 API 的 `related_scenarios` 声明,本侧不重复)
- **覆盖它的自动化**:待补

## 前置条件
- 已存在一个资金供应商(FundProvider)配置。
- 商户已在外部 MPGS Onboarding Portal 线下完成登记(待回传)。

## 操作步骤
1. 在 basis FundProvider 配置页把该供应商 `register_type` 设为 `MANUAL`。
2. 调 [[api_onboarding_get_config]],确认返回 `registerType=Manual` 且 `onboardingRuleList` 为空,人工登记规则字段(来自 `t_manual_register_rule` / `t_manual_register_rule_field`)正确渲染。
3. 在人工录入弹窗按规则填写商户 / 门店 / 设备(MERCHANT / STORE / DEVICE)登记信息并提交,触发 [[api_onboarding_manual_register]]。
4. 重复提交同一 key 的数据,验证覆盖写入。
5. 构造写入失败(如必填字段缺失),验证抛错行为。

## DB 校验点
- [[tbl_onboarding_t_fund_provider]]:`register_type = MANUAL`。
- 登记 item 与 item_result_map:写入成功且状态为「激活」;同 key 覆盖而非重复插入。
- 不产生 OnboardingOrder 记录(方案三:不走订单流转)。具体物理表名待补。

## 预期结果
- `registerType=Manual` 时 `onboardingRuleList` 为空,改用人工登记规则字段校验(如 mandatory)。
- 人工录入数据被转换为 item + item_result_map 并激活;同 key 覆盖。
- 自动报备流程不受影响(自动/手动隔离)。
- 写入失败时抛错,便于上游重试。
> 不确定 / 缺失的点(具体 item/item_result_map 物理表名、错误码、自动化覆盖)标「待补」。
