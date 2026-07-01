---
id: api_kyc_inquire_info
object_type: API
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:c77c6bdf-23d4-4c31-b325-128a8f8a6d3e
tags:
- KYC
- EID
- Passport
subdomain: eid-kyc
module: active-account
sensitivity: normal
name: 查询KYC信息接口 (inquire-info)
aliases:
- /kyc/active-account/v1/kyc/inquire-info
related_services:
- svc_kyc
related_tables:
- tbl_kyc_tm_kyc_apply
- tbl_kyc_tm_biz_record
related_scenarios:
- scn_kyc_status_inquire
- scn_kyc_eid_full_journey
---

## 用途
获取用户的 KYC 状态及对应的 EID/护照信息。根据 kycStatus 不同，决定是否返回 eidInfo / passportInfo；VIP 用户的敏感字段以 `******` 脱敏返回。

## 关联关系
- **所属服务**:[[svc_kyc]](related_services;api→service 边)
- **读写的表**:待补
- **被哪些场景测**:[[scn_kyc_status_inquire]]、[[scn_kyc_eid_full_journey]]
- **被哪些自动化覆盖**:[[auto_kyc_eid_journey]]

## 路径/方法
- API: `/kyc/active-account/v1/kyc/inquire-info`
- Method: POST
- Content-Type: JSON

## 入参
Request body 无显式必填业务参数（依赖会话/上下文身份）。

## 出参
Response body：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| kycStatus | String | Y | FINISH | NON：no kyc；PROCESS：用户正在做 kyc(ocr, liveness)，不返回 kyc 信息；FINISH：kyc 成功；EXPIRED：eid 过期（不含 buffer 期）；BLOCKED：拒绝 kyc，不返回信息；RESUBDOC：需重新提交 eid，不返回信息；AUDIT：风控等审核中，不返回信息 |
| token | String | N | 75762b77ed11445abd6078f739b53be7 | KYC flow id |
| eidInfo | EidInfo | N | — | EID 信息，VIP 显示 `******` |
| passportInfo | PassportInfo | — | — | 护照信息，VIP 显示 `******` |

eidInfo 字段：
- cardNo (String, N) — Eid 上的编号；VIP: `********`
- idNumber (String, Y) — EID number；VIP: `***************`
- nameEnglish (String, Y) — 英文名；VIP: `********`
- nameArabic (String, N) — 阿拉伯文名
- gender (String, Y) — 性别
- birthDate (String, Y) — 生日，yyyy-MM-dd
- nationality (String, Y) — 国籍
- religion (String, N) — 宗教
- marital (String, N) — 婚姻状态
- occupation (String, N) — 职业
- employer (String, N) — 雇主
- industry (String, N) — 行业
- effectTime (String, N) — 生效日期，yyyy-MM-dd
- invalidTime (String, Y) — 失效日期，yyyy-MM-dd
- renewFlag (String, Y) — Y/N

passportInfo 字段：
- passportType (String, Y) — 护照类型（Ordinary Passport-P / Diplomatic Passport-D / Official(Service) Passport-S/0 / Temporary Passport-TP / Refugee Passport-RP / Travel Document-TD / Seafarer's Passport-SP / Child Passport-CP / Emergency Passport-EP / United Nations Passport-UNP）
- nationality (String, Y) — 国籍
- name (String, Y) — 姓名
- passportNo (String, Y) — 护照号
- birthDate (String, Y) — 生日，yyyy-MM-dd
- gender (String, Y) — 性别
- address (String, Y) — 地址
- industry (String, N) — 行业
- invalidTime (String, Y) — 失效日期，yyyy-MM-dd
- renewFlag (String, Y) — Y/N

## 错误码
原文未列出本接口专属错误码。

## 测试校验点
- kycStatus = NON / PROCESS / BLOCKED / RESUBDOC / AUDIT 时，不应返回 eidInfo / passportInfo 详情。
- kycStatus = FINISH 时，eidInfo 必填字段（idNumber, nameEnglish, gender, birthDate, nationality, invalidTime, renewFlag）齐全。
- kycStatus = EXPIRED 时，需排除 buffer 期内的情形。
- VIP 用户：cardNo、idNumber、nameEnglish、以及 passportInfo 整体应按 `******` / `********` / `***************` 规则脱敏。
- 日期类字段格式为 `yyyy-MM-dd`（birthDate / effectTime / invalidTime）。
- renewFlag 取值仅 Y/N。
- passportType 返回值需在受支持的枚举集合内（P/D/S/0/TP/RP/TD/SP/CP/EP/UNP）。
- token 在状态为 PROCESS/FINISH 等流转中存在时应回传，可与后续 get-result / confirm-info / submit-edit 接口串联。
