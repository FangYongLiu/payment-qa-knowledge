---
id: api_sgs_place_mobile_order_prepaid
object_type: API
domain: life-center
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/843841543
tags:
- mobile-topup
- prepaid
- SGS
subdomain: mobile-topup
module: null
sensitivity: normal
name: 预付话费下单接口
aliases:
- Place mobile order - Prepaid
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
用于 SGS 预付话费充值场景下，提交话费充值订单（Place mobile order - Prepaid）。属于 Mobile Top-up 流程中下单环节，通常在完成 Query prepaid mobile Top-up 查询之后调用。

## 路径/方法
原文未提供具体路径与 HTTP 方法（仅以图片形式给出接口说明 image-20241203-100221.png）。

## 入参
原文未以文本形式列出入参字段，详见原文附图 image-20241203-100221.png。

## 出参
原文未以文本形式列出出参字段，详见原文附图 image-20241203-100221.png。

## 错误码
原文未提供错误码列表。

## 测试校验点
- 校验预付话费下单接口在 Query prepaid mobile Top-up 之后能正确提交订单。
- 与 Query prepaid international、Query prepaid mobile Top-up 等查询接口的入参/出参字段保持一致性（如手机号、面额、运营商等，具体以附图为准）。
- 其他字段级校验点原文未提供，待补充接口契约后完善。
