---
id: flow_life_center_mobile_topup
object_type: Flow
name: Life Center 话费充值端到端流程(SGS)
aliases: [Mobile Top-up Flow, SGS 话费充值流程]
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/843841543
tags: [mobile-topup, life-center, sgs, flow]
related_services: [svc_life_center, svc_query, svc_sgs]
related_tables: []
related_scenarios: [scn_life_center_mobile_topup]
---

# Life Center 话费充值端到端流程(SGS)

## 概述
Life Center 生活服务中的话费充值(Mobile Top-up)端到端链路:从用户发起查询(国际/本地预付、后付账单),到预付场景下提交充值订单,经由 SGS 对接外部渠道。起点 = 用户在 Life Center 查询话费;终点 = 预付订单提交(下单)。

## 步骤(跨系统)
1. [[svc_life_center]] → [[svc_query]] / [[svc_sgs]]:按业务类型发起查询
   - 国际预付:[[api_sgs_query_prepaid_international]](Query prepaid international)
   - 本地预付:[[api_sgs_query_prepaid_mobile_topup]](Query prepaid mobile Top-up)
   - 后付账单:[[api_sgs_query_postpaid_mobile_bill]](Query postpaid mobile bill)
2. (预付路径)[[svc_life_center]] → [[svc_sgs]]:在查询返回可充信息后,调用 [[api_sgs_place_mobile_order_prepaid]](Place mobile order - Prepaid)提交话费充值订单。

## 关联关系
- **经过的服务(有序)**:[[svc_life_center]] → [[svc_query]] / [[svc_sgs]](= `related_services`)
- **关键表**:待补(= `related_tables`)
- **关键场景**:[[scn_life_center_mobile_topup]](= `related_scenarios`)

## 校验点
- 查询接口与下单接口之间的数据/状态衔接是否一致(手机号、面额、运营商等入参在查询与下单间保持一致)。
- 预付(Prepaid)与后付(Postpaid)路径区分;国际(international)与本地(mobile Top-up)预付查询差异。
- 关键落库 / 状态流转 / 对账点:待补(原文以流程图截图 image-20241203-* 呈现,未给出文本细节)。
