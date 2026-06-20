---
id: api_member_change_mobile_refresh_kyc
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1751384142
tags:
- Dubbo
- KYC
- ChangeMobile
subdomain: change-mobile
module: member-identity
sensitivity: normal
name: 变更手机并刷新KYC接口
aliases:
- IMemberIdentityFacade#changeMobileAndRefreshKyc
- Member release & change mobile account
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
释放并切换会员手机号，同时刷新该会员的 KYC 信息。用于 EID Change Mobile 流程中：把 newMemberId 上的手机号释放，并将其绑定到 originalMemberId 选定的钱包账户上，写入最新 KYC 资料。

## 路径/方法
- 类型：Dubbo api
- 接口：`com.uaepay.member.service.facade.IMemberIdentityFacade#changeMobileAndRefreshKyc`

## 入参

| Parameter | Data Type | Mandatory | Sample | description |
|---|---|---|---|---|
| originalMemberId | String | Y | 100000436196 | Select the wallet ID (member ID) for the change mobile number |
| newMemberId | String | Y | 100000436197 | The wallet ID (member ID) that needs to be released |
| newKycInfo | KycInfo | Y |  | The new kyc information |

newKycInfo (KycInfo) 字段：

| Parameter | Data Type | Mandatory | Sample |
|---|---|---|---|
| unifiedNo | String | N | 252604500 |
| idNumber | String | Y | P393177663:=7*************8 |
| realName | String | Y | P393179435:=RAHEES****** |
| nameArabic | String | Y | P393177664 |
| nameEnglish | String | Y | P393179435:=RAHEES****** |
| familyNameAr | String | N | اشرف |
| familyNameEn | String | Y | ASHARAF |
| nationality | String | Y | India |
| nationalityCode | String | Y | IN |
| nationalityDesc | String | N | INDIAN |
| photo | String | N |  |
| birthDate | String | Y | 19991107 |
| maritalStatus | String | Y | 1 |
| religion | String | N | 1 |
| gender | String | Y | 1 |
| reserveMobile | String | N | P125092376 |
| effectTime | String | N |  |
| invalidTime | String | Y | 20270814 |
| partnerId | String | Y | 200000000005 |
| source | String | Y | eid |
| attachs | List<KycAttach> | Y |  |
| occupation | String | N | Stall And Market Salesperson |
| employer | String | N | Lulu Hypermarket, L L C, Branch Of Abu |
| issuePlace | String | N | Abu Dhabi |
| issueDate | Date | N |  |
| cardNo | String | N | 2312313 |
| industry | String | N | Retail |
| passportInfo | String | N | {"passportNo":"P393179094","expiryDate":"20280904","nationalityCode":"IN","nationalityDesc":"INDIAN","passportType":"Normal Passport"} |
| scene | String | N | changeMobile |
| extension | Map | N | {"issuePlaceArabic":"دبي","employerArabic":"...","occupationArabic":"..."} |

## 出参
原文未列出具体响应字段（Response 表格为空）。

## 错误码
原文未给出。

## 测试校验点
- originalMemberId、newMemberId 必填，分别代表"选定接收手机号的钱包"与"被释放手机号的钱包"，二者不可混淆。
- newKycInfo 中标 Y 的字段（idNumber/realName/nameArabic/nameEnglish/familyNameEn/nationality/nationalityCode/birthDate/maritalStatus/gender/invalidTime/partnerId/source/attachs）必须有值。
- source 取值 `eid`；scene 取值 `changeMobile`，与变更手机场景一致。
- 验证执行后：newMemberId 上的手机号被释放，originalMemberId 成功绑定该手机号，且 KYC 信息按 newKycInfo 刷新。
- 与 [[api_member_query_eid_bound_account]] 返回的 memberAccountList（mobileTicket、memberId）联动校验：originalMemberId 应来自该列表中用户选定的账户。
- 与 [[api_kyc_eid_confirm_change_mobile]] 流程衔接：本接口成功后，confirm-change-mobile 才会返回 Change Mobile Success 的 tips。
- passportInfo、extension 等 JSON/Map 字段格式按样例解析，不可破坏 Arabic 文本编码。
