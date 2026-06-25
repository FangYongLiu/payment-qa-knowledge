---
id: scn_life_center_mobile_topup
object_type: Scenario
name: Mobile Top-up 话费充值(SGS)
aliases: [话费充值, Mobile Top-up, 生活缴费-话费]
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/843841543
tags: [mobile-topup, life-center, sgs]
related_services: [svc_life_center, svc_sgs, svc_query]
related_tables: []
related_logs: []
---

# Mobile Top-up 话费充值(SGS)

Life Center 生活服务下的话费充值场景:通过 SGS 对接,完成预付/后付话费的查询与下单。覆盖国际预付、本地预付、后付费账单三类查询,以及预付下单。

## 触发 / 入口
- 用户在 Life Center 发起话费充值/账单查询。
- 入口接口(SGS 对接):
  - [[api_sgs_query_prepaid_international]]:查询国际预付话费(Query prepaid international)
  - [[api_sgs_query_prepaid_mobile_topup]]:查询本地预付话费充值(Query prepaid mobile Top-up)
  - [[api_sgs_query_postpaid_mobile_bill]]:查询后付费话费账单(Query postpaid mobile bill)
  - [[api_sgs_place_mobile_order_prepaid]]:预付话费下单(Place mobile order - Prepaid)

## 关联关系
- **涉及服务**:[[svc_life_center]] → [[svc_sgs]] / [[svc_query]](= `related_services`)
- **校验的表**:待补
- **相关日志**:待补
- **端到端流程**:[[flow_life_center_mobile_topup]]

## 前置条件
- 待补(账户/手机号/运营商基础数据)。

## 操作步骤
1. 按业务类型选择查询接口:
   - 国际预付 → Query prepaid international
   - 本地预付 → Query prepaid mobile Top-up
   - 后付账单 → Query postpaid mobile bill
2. 预付场景:查询返回可充面额/价格后,调用 Place mobile order - Prepaid 提交下单。

## DB 校验点
- 待补(下单落库表与状态流转,原文以截图呈现未给出文本细节)。

## 预期结果
- 查询接口正确返回可充信息;预付下单在查询之后能正确提交订单。
- 边界区分:Prepaid(预付)与 Postpaid(后付)处理路径不同;国际(international)与本地(mobile Top-up)预付查询有差异。
> 字段、错误码、状态等原文以流程图/截图(image-20241203-*)呈现,未给出文本细节,标「待补」。
