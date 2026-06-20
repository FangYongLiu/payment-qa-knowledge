---
id: api_kyc_inquire_info
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1089405294
tags:
- KYC
- EID
- Passport
subdomain: eid-kyc
module: active-account
sensitivity: normal
name: 查询KYC信息接口
aliases:
- Inquire kyc information
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
获取用户 KYC 信息，包括 KYC 状态、EID 信息（eidInfo）以及护照信息（passportInfo）。VIP 用户的敏感字段以 `******` 形式打码返回。

## 路径/方法
- API: `/kyc/active-account/v1/kyc/inquire-info`
- Method: POST

## 入参
Request body 无业务参数（文档中未列出任何字段）。

## 出参
Response body：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| kycStatus | String | Y | FINISH | KYC 状态：NON / PROCESS / FINISH / EXPIRED / BLOCKED / RESUBDOC / AUDIT |
| token | String | N | 75762b77ed11445abd6078f739b53be7 | KYC flow id |
| eidInfo | EidInfo | N | - | EID 信息，VIP 显示 `******` |
| passportInfo | PassportInfo | - | - | Passport 信息，VIP 显示 `******` |

kycStatus 取值含义：
- NON：no kyc
- PROCESS：用户正在进行 kyc（ocr, liveness），不返回 kyc 信息
- FINISH：success kyc
- EXPIRED：eid expiry（不含 buffer period）
- BLOCKED：reject kyc，不返回 kyc 信息
- RESUBDOC：re-submit eid，不返回 kyc 信息
- AUDIT：如风险评级，不返回 kyc 信息

eidInfo 字段：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| cardNo | String | N | 136133886 | EID 上的 number；VIP：`********` |
| idNumber | String | Y | 7*************1 | EID number；VIP：`***************` |
| nameEnglish | String | Y | San*** | 英文名；VIP：`********` |
| nameArabic | String | N | العتيبه | 阿拉伯文名 |
| gender | String | Y | Male | 性别 |
| birthDate | String | Y | 1992-01-01 | 生日，yyyy-MM-dd |
| nationality | String | Y | India | 国籍 |
| religion | String | N | Muslim | 宗教 |
| marital | String | N | UnMarried | 婚姻状况 |
| occupation | String | N | Portnr | 职业 |
| employer | String | N | AlRiqah Spocialzed Dontal Centere | 雇主 |
| industry | String | N | Retail | 行业 |
| effectTime | String | N | 2024-12-01 | yyyy-MM-dd |
| invalidTime | String | Y | 2026-12-01 | yyyy-MM-dd |
| renewFlag | String | Y | Y | Y/N |

passportInfo 字段：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| passportType | String | Y | Ordinary Passport | 护照类型：P/D/S/0/TP/RP/TD/SP/CP/EP/UNP |
| nationality | String | Y | India | 国籍 |
| name | String | Y | San***** | 姓名 |
| passportNo | String | Y | E******E | 护照号 |
| birthDate | String | Y | 1992-01-01 | yyyy-MM-dd |
| gender | String | Y | Male | 性别 |
| address | String | Y | - | 地址 |
| industry | String | N | Media | 行业 |
| invalidTime | String | Y | 2026-12-01 | yyyy-MM-dd |
| renewFlag | String | Y | N | Y/N |

passportType 编码对照：
- 普通护照 Ordinary Passport - P
- 外交护照 Diplomatic Passport - D
- 公务护照 Official / Service Passport - S/0
- 临时护照 Temporary Passport - TP
- 难民护照 Refugee Passport - RP
- 旅行证 Travel Document - TD
- 海员护照 Seafarer's Passport - SP
- 儿童护照 Child Passport - CP
- 紧急护照 Emergency Passport - EP
- 联合国护照 United Nations Passport - UNP

## 错误码
原文未列出该接口的错误码。

## 测试校验点
- kycStatus 返回不同值时的字段裁剪行为：
  - PROCESS / BLOCKED / RESUBDOC / AUDIT 时不返回 kyc 信息（eidInfo / passportInfo 应不返回）
  - FINISH 时返回完整 eidInfo / passportInfo
  - EXPIRED 仅在不含 buffer period 时返回
  - NON 表示无 KYC
- VIP 用户敏感字段需以 `******` 形式打码：eidInfo.cardNo、idNumber、nameEnglish；passportInfo 整体显示 `******`
- 日期字段格式必须为 `yyyy-MM-dd`：birthDate、effectTime、invalidTime
- renewFlag 仅取 `Y` / `N`
- passportType 取值需在枚举范围内（P/D/S/0/TP/RP/TD/SP/CP/EP/UNP）
- token 字段需与 KYC flow id 一致（用于后续接口串联）
- Mandatory=Y 字段必须返回；Mandatory=N 字段允许缺省
