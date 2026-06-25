---
id: scn_kyc_eid_leave
object_type: Scenario
name: 放弃 EID 认证 journey
aliases: [test_kyc_eid_leave_journey]
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_KYC_eid_journey.py::test_kyc_eid_leave_journey
tags: [KYC, EID, leave, 放弃]
related_services: [svc_kyc]
related_tables: []
related_logs: []
---

# 放弃 EID 认证 journey

## 触发 / 入口
- 用户在 EID journey 中途放弃。入口接口 [[api_kyc_eid_leave_submit]]。
- 自动化用例:`test_kyc_eid_leave_journey`(EID journey TC7)。

## 关联关系
- **涉及服务**:[[svc_kyc]]
- **走过的接口**:[[api_kyc_eid_start_journey]](取 token)→ [[api_kyc_eid_leave_submit]]
- **覆盖它的自动化**:[[auto_kyc_eid_journey]]

## 前置条件
- 用户已 login;已 start-journey 拿到 `token`。

## 操作步骤
1. login。
2. start-journey → 取 `token`。
3. leave-submit(token + leave_reason)。

## DB 校验点
- 放弃原因落库 / journey 置为放弃态 —— **待补**(表未确认)。

## 预期结果
- 放弃成功(断言 `except_msg`)。
- 业务规则:放弃后**不可重提**(见 [[svc_kyc]] 说明)——该约束的回归**待补**。
