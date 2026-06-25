---
id: auto_kyc_profile
object_type: AutomationAsset
name: KYC 用户 Profile 查看自动化 (test_KYC_xinwei)
aliases: [TestKYC, test_KYC_xinwei]
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_KYC_xinwei.py
tags: [KYC, EID, Passport, VIP, profile, 脱敏, 自动化, cgs-apitest]
related_scenarios: [scn_kyc_profile_view]
related_services: [svc_kyc]
related_tables: [tbl_member_tm_member, tbl_member_tm_passport_entity, tbl_member_tm_realname_entity, tbl_member_tr_bank_account, tbl_member_tr_member_kyc_level, tbl_member_tr_verify_ref]
---

# KYC 用户 Profile 查看自动化

> 来源:cgs-apitest 回归套件 `test_KYC_xinwei.py`(`TestKYC`,作者 Zongting Mao,2024-04-29,7 个 TC)。
> 覆盖**不同 KYC 状态/等级的用户查看认证 Profile** + 限额 + 关键字段 DB 校验。

## 用途
验证认证中心(verify center)对各类用户的 Profile 渲染与落库一致性。覆盖 7 类用户:

| TC | 用户类型 | 覆盖点 |
| --- | --- | --- |
| 1 | EID 已认证(有效) | kycInfo 字段齐全;realname_entity / verify_ref 落库一致 |
| 2 | EID 已过期 | EID expiry 下仍能查 Profile;同样校验落库 |
| 3 | 未 KYC(NON,未绑卡) | `kycStatus":"NON_KYC"`;可查限额 |
| 4 | CDD0(未 KYC,已绑卡) | sva 状态 UNACTIVE;kyc_level=0;绑卡列表 + 银行账户落库 |
| 5 | Passport 用户 | `passportStatus":"FINISH"`;passportInfo 字段 + passport_entity 落库 |
| 6 | VIP | memberLevel 校验;`tm_member.cps_type='VIP'` |
| 7 | VVIP | 同 VIP 校验 |

## 关联关系
- **覆盖的场景**:[[scn_kyc_profile_view]](各用户类型变体)
- **针对/跑在的服务**:[[svc_kyc]](实名认证域)——⚠️ 注意入口接口走 **personal/钱包 facade**(`personal_kyc_router`、`personal_kyc_verifyCenterInit`、`personal_common_queryUserLimit`、`personal_sva_queryStatusInfo`、`personal_kyc_queryPaymentCardList`),内部读 KYC 数据;**不是** kyc 服务的 journey 接口。
- 与 [[auto_kyc_eid_journey]] 互补:那个测"怎么认证",这个测"认证后/各状态怎么展示"。

## 使用方式
- 框架:pytest + allure;入口 `pytest testcases/payment/basic_cases/test_KYC_xinwei.py`。
- markers:`sim`。
- 依赖夹具:`get_urls`、`get_env_data`、`db_instance_factory`、`get_testdata`、`Module`、`CGSapi`。
- 测试数据按方法名取(如 `test_EID_KYC_profile` 的 partner_id/uid/mobile_no/except_msg/kyc_msg)。

## 关键配置
- **DB 校验表**(`member` 库):
  - `member.tm_realname_entity` + `member.tr_verify_ref`(EID 实名实体 + 校验引用)
  - `member.tm_passport_entity`(护照实体,passport_type/nationality/no/expiry)
  - `member.tm_member`(`cps_type`/`CPS_TYPE`:NORMAL→N / VIP→V,等级校验)
  - `member.tr_member_kyc_level`(kyc_level=0 表示 CDD0/未认证)
  - `member.tr_bank_account`(绑卡校验)
- **脱敏对照(ticket)**:敏感字段以 `CONCAT(<ticket>,':=',<明文>)` 存库——
  `real_name = CONCAT(nameTicket, ':=', name)`、`id_number = CONCAT(idNumberTicket, ':=', idNumber)`、护照同理。校验时需用 ticket+明文拼接比对。

## 注意事项
- 这是**展示/读取侧**回归,不触发实名认证流程(那在 [[auto_kyc_eid_journey]])。
- TC3 的 step4 DB 校验被注释掉(NON 用户 KYC 落库断言),现状只校验 kycStatus 文案 + 限额——**待补/待确认**是否需恢复。
- 限额断言统一靠文案 `"title":"Max. Single Transaction"`。
- 更多 flaky/数据坑 **待补**。
