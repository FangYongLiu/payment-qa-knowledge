---
id: scn_kyc_status_inquire
object_type: Scenario
name: KYC 状态查询与提醒 (FINISH / NON / reminder)
aliases: [test_kyc_eid_check_reminder, test_kyc_eid_inquire_info_finish, test_kyc_eid_inquire_info_non]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_KYC_eid_journey.py
tags: [KYC, 状态查询, reminder]
related_services: [svc_kyc]
related_tables: []
related_logs: []
---

# KYC 状态查询与提醒

## 触发 / 入口
- 查询用户当前 KYC 状态,或对已完成用户做提醒确认。入口接口 [[api_kyc_inquire_info]] / [[api_kyc_check_reminder]]。
- 自动化用例:`test_kyc_eid_check_reminder`(TC1)、`test_kyc_eid_inquire_info_finish`(TC2)、`test_kyc_eid_inquire_info_non`(TC3)。

## 关联关系
- **涉及服务**:[[svc_kyc]]
- **走过的接口**:[[api_kyc_inquire_info]]、[[api_kyc_check_reminder]]
- **覆盖它的自动化**:[[auto_kyc_eid_journey]]

## 前置条件
- 已 login。变体:已认证用户(FINISH)/ 新建未认证用户(NON)。

## 操作步骤
1. login。
2. inquire-info → 读 `body.kycStatus`;或 check-reminder(scene)→ 验提醒文案。

## DB 校验点
- 状态查询为只读,无落库断言。

## 预期结果
- 响应含 `apply success`。
- `kycStatus`:已认证=`FINISH`(body 含 `eidInfo` 或 `passportInfo`);新用户=`NON`。
- check-reminder 返回预期提醒文案。
