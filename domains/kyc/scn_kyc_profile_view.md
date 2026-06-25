---
id: scn_kyc_profile_view
object_type: Scenario
name: KYC 认证 Profile 查看(各用户类型)
aliases: [test_EID_KYC_profile, test_passport_KYC_profile, test_VIP_KYC_profile]
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_KYC_xinwei.py
tags: [KYC, profile, EID, Passport, VIP, 脱敏, 限额]
related_services: [svc_kyc]
related_tables: [tbl_member_tm_member, tbl_member_tm_passport_entity, tbl_member_tm_realname_entity, tbl_member_tr_bank_account, tbl_member_tr_member_kyc_level, tbl_member_tr_verify_ref]
related_logs: []
---

# KYC 认证 Profile 查看(各用户类型)

## 触发 / 入口
- 用户进入认证中心查看 KYC Profile。入口接口 `personal_kyc_verifyCenterInit`(**personal/钱包 facade**,非 kyc 服务直接接口;内部读 KYC 数据)。
- 自动化用例:`test_KYC_xinwei.py`(TC1–7)。

## 关联关系
- **涉及服务**:[[svc_kyc]](KYC 数据来源域);入口经 personal facade。
- **校验的表**:`member.*`(见下,tbl 对象**待补**)
- **覆盖它的自动化**:[[auto_kyc_profile]]

## 前置条件
- 已 login。按**用户类型变体**取测试数据:

| 变体 | 断言要点 |
| --- | --- |
| EID 有效 | kycInfo 字段齐全(unifiedNo/name/idNumber/memberLevel) |
| EID 过期 | EID expiry 下仍可查 Profile |
| NON(未 KYC,未绑卡) | `kycStatus":"NON_KYC"` |
| CDD0(未 KYC,已绑卡) | sva `UNACTIVE`;`kyc_level=0`;绑卡列表非空 |
| Passport | `passportStatus":"FINISH"`;passportInfo 字段 |
| VIP / VVIP | `memberLevel`;`cps_type='VIP'` |

## 操作步骤
1. login。
2. personal-kyc-router → 验页面文案。
3. personal-kyc-verifyCenterInit → 取 `kycInfo` / `passportInfo`。
4. DB 校验(见下)。
5. personal-common-queryUserLimit → 限额含 `"title":"Max. Single Transaction"`。

## DB 校验点
- `member.tm_realname_entity` + `member.tr_verify_ref`(EID 实名实体 + 校验引用)。
- `member.tm_passport_entity`(护照:passport_type/nationality/no/expiry)。
- `member.tm_member`(`cps_type`:NORMAL→N / VIP→V,等级校验)。
- `member.tr_member_kyc_level`(`kyc_level=0` = CDD0/未认证)。
- `member.tr_bank_account`(绑卡)。
- **脱敏 ticket**:敏感字段以 `CONCAT(<ticket>,':=',<明文>)` 存库(`real_name`/`id_number`/护照同理),校验需拼接比对。
- 以上 tbl 对象均**待补**。

## 预期结果
- 各用户类型的 `kycStatus`/`passportStatus`/`memberLevel` 渲染与落库一致;限额正常返回。
- 注:TC3(NON)的 DB 校验在代码中被注释,现状只校验文案+限额——**待确认**是否恢复。
