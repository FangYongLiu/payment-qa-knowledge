---
id: api_sgs_query_postpaid_mobile_bill
object_type: API
domain: life-center
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/843841543
tags:
- SGS
- Mobile Top-up
- Postpaid
subdomain: mobile-topup
module: SGS
sensitivity: normal
name: 查询后付费话费账单接口
aliases:
- Query postpaid mobile bill
related_services: []
related_tables: []
related_scenarios:
- life-center-sgs-api-overview
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
SGS Mobile Top-up 模块下的"查询后付费话费账单"接口，用于查询后付费手机号当前应缴账单信息（如账单金额、账期、应缴费等），为后续话费缴纳/下单提供账单依据。

## 路径/方法
原文未给出具体 HTTP 路径与方法（仅以流程图 image-20241203-100138.png 形式展示），待补充。

## 入参
原文未列出字段级入参定义，待补充。

## 出参
原文未列出字段级出参定义，待补充。

## 错误码
原文未列出错误码定义，待补充。

## 测试校验点
- 校验后付费手机号能正确返回账单信息（账期、应缴金额等关键字段）。
- 校验非后付费号码 / 不存在号码 / 无账单号码时的返回与错误处理。
- 校验该接口与同模块其他接口（Query prepaid international、Query prepaid mobile Top-up、Place mobile order - Prepaid）的边界区分，确保只处理后付费账单查询场景。
- 具体字段级与错误码校验点待原文补充字段定义后完善。
