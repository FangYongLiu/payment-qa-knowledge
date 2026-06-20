---
id: api_member_change_mobile_refresh_kyc
object_type: API
domain: kyc
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:2654d3b2-24d5-481b-926b-96f41f946ae8
tags:
- dubbo
- kyc
- change-mobile
subdomain: change-mobile
module: member-identity
sensitivity: normal
name: 释放并换绑手机号刷新KYC接口 (changeMobileAndRefreshKyc)
aliases:
- IMemberIdentityFacade#changeMobileAndRefreshKyc
related_services: []
related_tables: []
related_scenarios:
- kyc-change-mobile-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
Member Dubbo 接口，用于在 KYC 换绑手机号场景下：将原 memberId（originalMemberId）持有的手机号释放，改绑到新的 memberId（newMemberId），同时使用新的 KYC 信息（newKycInfo）刷新会员的 KYC 数据。

## 路径/方法
- 接口类：`com.uaepay.member.service.facade.IMemberIdentityFacade`
- 方法：`changeMobileAndRefreshKyc`
- 协议：Dubbo

## 入参
| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| originalMemberId | String | Y | 100000436196 | Select the wallet ID (member ID) for the change mobile number |
| newMemberId | String | Y | 100000436197 | The wallet ID (member ID) that needs to be released |
| newKycInfo | KycInfo | Y | - | The new kyc information |

newKycInfo（KycInfo）字段：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| unifiedNo | String | N | 252604500 | |
| idNumber | String | Y | P393177663:=7*************8 | |
| realName | String | Y | P393179435:=RAHEES****** | |
| nameArabic | String | Y | P393177664 | |
| nameEnglish | String | Y | P393179435:=RAHEES****** | |
| familyNameAr | String | N | اشرف | |
| familyNameEn | String | Y | ASHARAF | |
| nationality | String | Y | India | |
| nationalityCode | String | Y | IN | |
| nationalityDesc | String | N | INDIAN | |
| photo | String | N | | |
| birthDate | String | Y | 19991107 | |
| maritalStatus | String | Y | 1 | |
| religion | String | N | 1 | |
| gender | String | Y | 1 | |
| reserveMobile | String | N | P125092376 | |
| effectTime | String | N | | |
| invalidTime | String | Y | 20270814 | |
| partnerId | String | Y | 200000000005 | |
| source | String | Y | eid | |
| attachs | List<KycAttach> | Y | | |
| occupation | String | N | Stall And Market Salesperson | |
| employer | String | N | Lulu Hypermarket, L L C, Branch Of Abu | |
| issuePlace | String | N | Abu Dhabi | |
| issueDate | Date | N | | |
| cardNo | String | N | 2312313 | |
| industry | String | N | Retail | |
| passportInfo | String | N | {"passportNo":"P393179094","expiryDate":"20280904","nationalityCode":"IN","nationalityDesc":"INDIAN","passportType":"Normal Passport"} | |
| scene | String | N | changeMobile | changeMobile |
| extension | Map | N | {"issuePlaceArabic":"دبي","employerArabic":"...","occupationArabic":"..."} | Extension |

## 出参
原文 Response 表头列出 Parameters/Data Type/Mandatory/Sample/description，但未给出具体字段定义。

## 错误码
原文未列出。

## 测试校验点
- originalMemberId 与 newMemberId 必须有效，且二者关系正确：原 memberId 持有的手机号被释放，新 memberId 完成换绑。
- newKycInfo 中标记为 Y 的必填字段全部传入（idNumber、realName、nameArabic、nameEnglish、familyNameEn、nationality、nationalityCode、birthDate、maritalStatus、gender、invalidTime、partnerId、source、attachs 等）。
- source=eid、scene=changeMobile 场景下，KYC 信息按 EID 来源刷新到新 memberId。
- 调用成功后，新 memberId 的 KYC 信息被更新为传入的 newKycInfo；原 memberId 的手机号绑定关系被释放。
- 与上游接口 [[api_kyc_confirm_change_mobile]] 串联，并基于 [[api_member_query_eid_bound_account]] 查询到的 memberAccountList 选择 originalMemberId/newMemberId。
- 整体流程参见 [[kyc-change-mobile-flow]]。
