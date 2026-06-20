---
title: Life Center SGS API 流程总览
domain: life-center
kind: wiki_page
slug: life-center-sgs-api-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/843841543
tags: []
---

# Life Center SGS API 流程总览

本页汇总 [[domain_life_center]] 场景下 SGS 对接的 API 分类与流程索引，便于按主题快速定位各接口的查询与下单链路。

## Mobile Top-up

围绕话费充值场景，SGS 提供以下四类接口：

- [[api_sgs_query_prepaid_international]]：查询国际预付话费（Query prepaid international）
- [[api_sgs_query_prepaid_mobile_topup]]：查询本地预付话费充值（Query prepaid mobile Top-up）
- [[api_sgs_query_postpaid_mobile_bill]]：查询后付费话费账单（Query postpaid mobile bill）
- [[api_sgs_place_mobile_order_prepaid]]：预付话费下单（Place mobile order - Prepaid）

### 接口分组说明

- **查询类**：
  - 国际预付：`Query prepaid international`
  - 本地预付：`Query prepaid mobile Top-up`
  - 后付费账单：`Query postpaid mobile bill`
- **下单类**：
  - 预付话费下单：`Place mobile order - Prepaid`

各接口的详细字段、流程图与交互细节请进入对应子页面查看。
