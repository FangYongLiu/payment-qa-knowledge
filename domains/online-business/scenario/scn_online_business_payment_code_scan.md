---
id: scn_online_business_payment_code_scan
object_type: Scenario
name: 付款码被扫线下收单 (POS / 扫码枪)
aliases: [付款码支付, payment-code-scan, scan-to-pay]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: legacy/domains/payby-open-api(payment_code_scanned_by_pos / by_scanner)
tags: [online-business, 付款码, 线下收单, SGS, acquire]
related_services: [svc_sgs, svc_acquireii]
related_tables: []
related_logs: []
---

# 付款码被扫线下收单 (POS / 扫码枪)

> 业务测试场景。来源:legacy payby-open-api 两篇时序(POS 机扫 / 扫码枪扫,链路一致,合并为一条)。

## 触发 / 入口
用户在结账时向商户出示 PayBy 付款码,商户用扫码设备扫描后由商户后端调 SGS 下单接口发起线下收单交易。扫码设备有两类,链路相同:
- **smart POS**:商户用智能 POS 扫码设备扫描并解析付款码。
- **扫码枪 (scanner)**:商户用扫码枪等设备扫描并解析付款码。

## 关联关系
- **涉及服务**:[[svc_sgs]](开放网关/中介)、[[svc_acquireii]](收单)(= `related_services`)。SGS 在流程中作为商户后端与 acquire 之间的代理。
- **读写的表**:待补(收单订单落 acquireii 系列表,具体表待补)。
- **相关日志**:`service:sgs` / `service:acquireii`(= `related_logs`,排障定位用)。

## 前置条件
- 用户已生成可用的付款码并展示。
- 商户具备扫码设备(smart POS 或扫码枪),可扫描并解析付款码。
- 商户后端已对接 SGS 下单接口,并具备接收异步通知的能力。
- SGS 与 acquire 之间链路可用。

## 操作步骤
1. 用户出示付款码。
2. 商户用扫码设备(POS / 扫码枪)扫描并解析用户付款码。
3. 商户后端 → SGS:请求下单接口,传入解析得到的用户付款码。
4. SGS → acquire:转发请求下单接口。
5. acquire → SGS:返回下单结果。
6. SGS → 商户后端:返回下单结果(同步响应链路完成)。
7. acquire → SGS:异步通知支付结果。
8. SGS → 商户后端:异步通知支付结果(异步链路,见 [[scn_online_business_merchant_async_notify]])。

## DB 校验点
- 收单订单落库、状态流转:待补(原文未提供具体表/字段)。

## 预期结果
- **同步链路**:商户后端通过 SGS 调用 acquire 下单成功,拿到下单结果。
- **异步链路**:acquire 通过 SGS 将最终支付结果异步回传商户后端,完成 smart POS / 扫码枪扫付款码方式的线下收单交易。
- POS 扫与扫码枪扫两种入口对后端链路无差异,差异仅在前端扫码设备。
