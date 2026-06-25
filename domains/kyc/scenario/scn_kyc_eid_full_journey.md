---
id: scn_kyc_eid_full_journey
object_type: Scenario
name: EID 完整实名认证 journey (NON→FINISH)
aliases: [test_kyc_eid_full_journey]
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_KYC_eid_journey.py::test_kyc_eid_full_journey
tags: [KYC, EID, 实名认证, journey]
related_services: [svc_kyc]
related_tables: [tbl_member_tr_member_kyc_level]
related_logs: []
---

# EID 完整实名认证 journey (NON→FINISH)

## 触发 / 入口
- NON-KYC 用户发起 EID(阿联酋身份证)实名认证。入口接口 [[api_kyc_eid_start_journey]]。
- 自动化用例:`test_kyc_eid_full_journey`(EID journey TC6)。

## 关联关系
- **涉及服务**:[[svc_kyc]](实名认证)
- **校验的表**:`member.tr_member_kyc_level`(tbl 对象**待补**)
- **走过的接口**:[[api_kyc_inquire_info]] → [[api_kyc_eid_start_journey]] → [[api_kyc_eid_get_result]] → [[api_kyc_eid_inquire_industry]] → [[api_kyc_eid_confirm_info]]
- **覆盖它的自动化**:[[auto_kyc_eid_journey]]

## 前置条件
- 用户已注册,`kycStatus=NON`。
- SIM 环境 Signzy journey 自动完成;**UAT 需在 start-journey 与 get-result 之间手工完成 Signzy**。

## 操作步骤
1. login(partner_id / uid / mobile_no)。
2. inquire-info → 断言 `kycStatus=NON`。
3. start-journey → 返回 `commandType=moveForward` + journey `token`。
4. (Signzy 完成后)get-result → `commandType=action` 时带 `eidInfo`。
5. inquire-industry → 行业列表非空,选一个 industry。
6. confirm-info(token + industry)。
7. inquire-info → 断言 `kycStatus ∈ {FINISH, PROCESS}`。

## DB 校验点
- `member.tr_member_kyc_level`:存在该 member 的记录;认证有效时 `kyc_level=2` / `status=VALID`(见 TC8 mock 用户)。tbl 对象**待补**。

## 预期结果
- `kycStatus` 由 `NON` → `FINISH`(或 `PROCESS`);`eidInfo` 落库;后续限额提升。
- 失败分支(OCR/活体失败、过期)**待补**。
