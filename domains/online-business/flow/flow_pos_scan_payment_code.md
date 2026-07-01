---
id: flow_pos_scan_payment_code
object_type: Flow
name: 付款码被 POS 机扫(线下被扫收单)端到端流程
aliases: [付款码被扫, POS scan payment code, smart pos 被扫]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki_image:aface4c4 (付款码被POS机扫场景)
tags: [online-business, acquiring, POS, 付款码, 被扫]
related_services: [svc_pos_gateway, svc_acquireii]
related_tables: [tbl_acquireii_t_acquire_order]
related_scenarios: [scn_online_business_cashier_pay]
---

# 付款码被 POS 机扫(线下被扫收单)端到端流程

## 概述
用户结账时出示付款码(QRPAY),商户用 smart pos 扫码设备扫描发起线下收单。起点 = 用户出示付款码;终点 = smart pos 经 pos-gateway → acquire 完成下单并轮询到支付结果。

## 步骤(跨系统)
1. 用户出示付款码。
2. 商户用 smart pos 扫描用户付款码。
3. smart pos → [[svc_pos_gateway]](扫码并请求下单接口)。
4. [[svc_pos_gateway]] → [[svc_acquireii]](转发下单请求)。
5. [[svc_acquireii]] 处理下单 → 返回下单结果给 [[svc_pos_gateway]]。
6. [[svc_pos_gateway]] 将下单结果返回 smart pos。
7. smart pos → [[svc_pos_gateway]] 发起轮询支付结果。
8. [[svc_pos_gateway]] → [[svc_acquireii]] 转发轮询请求。

> 注:原图未画出轮询请求的响应箭头(标「待补」)。

## 关联关系
- **经过的服务(有序)**:smart pos → [[svc_pos_gateway]] → [[svc_acquireii]](= `related_services`)。
- **关键表**:[[tbl_acquireii_t_acquire_order]](= `related_tables`)。
- **关键场景**:[[scn_online_business_cashier_pay]](收银台/受理面支付,含 QRPAY 付款码形态)。

## 校验点
- smart pos 经 pos-gateway → acquire 能完成下单并收到下单结果。
- 轮询链路 smart pos → pos-gateway → acquire 能取到支付结果。
- 落库 `t_acquire_order`、支付终态;DB 校验点原文未提供(标「待补」)。
