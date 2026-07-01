---
id: scn_kyc_zand_iban
object_type: Scenario
name: KYC 用户分配 ZAND IBAN
aliases: [test_e2e_new_user_to_zand_iban, test_zand_iban_assigned]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_KYC_eid_journey.py
tags: [KYC, ZAND, IBAN, VA, 钱包]
related_services: [svc_kyc]
related_tables: []
related_logs: []
---

# KYC 用户分配 ZAND IBAN

## 触发 / 入口
- KYC FINISH 用户开通 / 验证 ZAND 虚拟账户(IBAN)。
- 自动化用例:`test_e2e_new_user_to_zand_iban`(TC10,新用户全自动)、`test_zand_iban_assigned`(TC11,白名单真实用户)。

## 关联关系
- **涉及服务**:[[svc_kyc]](实名认证是前置);ZAND VA / 钱包侧接口属 personal/ZAND 服务(非 kyc 接口)。
- **校验的表**:`visii.t_va`(tbl 对象**待补**)
- **覆盖它的自动化**:[[auto_kyc_eid_journey]]

## 前置条件
- 用户已 KYC `FINISH`。
- TC10:真实 Signzy 实体 + `vam_auth_active` bypass;TC11:用户在 `VISII_KYC_MID_WHITELIST` 白名单(真实用户 `1TZHXRCM` / member `100000091371`)。

## 操作步骤
1. (新用户)create-zand-kyc-user;或(白名单)get-zand-kyc-user。
2. vam-auth-init → `openStatus=V`(TC11)。
3. vam-auth-query-info → `bankCode=ZAND` / `bankName=zand bank` / `accountType=BASIC` / `iban` 非空。
4. personal-sva-queryStatusInfo → 钱包 `statusCode=ACTIVATED`。

## DB 校验点
- `visii.t_va`(member_id + `bank_code='ZAND'`):`status='V'` / `iban` 非空 / `account_type=BASIC`。tbl 对象**待补**。

## 预期结果
- KYC FINISH 用户成功分配 ZAND IBAN,钱包激活(ACTIVATED)。
