---
id: api_sgs_query_prepaid_mobile_topup
object_type: API
domain: online-business
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/843841543
tags:
- mobile-topup
- prepaid
- query
subdomain: mobile-topup
module: null
sensitivity: normal
name: 查询本地预付话费充值接口
aliases:
- Query prepaid mobile Top-up
related_services:
- svc_query
---

## 用途
SGS Mobile Top-up 场景下用于查询本地预付话费充值的接口（Query prepaid mobile Top-up）。

## 路径/方法
原文未提供（仅以截图 image-20241203-100100.png 呈现）。

## 入参
原文未提供。

## 出参
原文未提供。

## 错误码
原文未提供。

## 测试校验点
- 验证本地预付话费充值查询流程能正确返回结果（具体字段以截图为准，原文未给出文本细节）。
- 与相关接口的边界区分：
  - 国际预付查询见 [[api_sgs_query_prepaid_international]]
  - 后付费账单查询见 [[api_sgs_query_postpaid_mobile_bill]]
  - 预付下单见 [[api_sgs_place_mobile_order_prepaid]]
- 整体流程参考 [[life-center-sgs-api-overview]]。
