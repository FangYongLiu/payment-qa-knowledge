---
id: svc_sgs
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp028
name: sgs
dev_owner: Yongxing.Cao
aliases: [gp028_sgs]
related_services: []
related_tables: []
related_scenarios: [scn_online_business_direct_pay]
---

# sgs

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp028` · domain=`payment-core`。

## 作用
(本窗口未观测到该服务的运行时活动,作用待业务补充。)

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
(本窗口未观测到与其它服务的调用关系)

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_sgs_place_mobile_order_prepaid]] 预付话费下单接口

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_direct_pay]](自动化:直连支付自动化)
- [[flow_botim_wallet_binding_auth]](流程:BOTIM 钱包绑定/登录/Token 刷新认证流程)
- [[flow_zand_fundout]](流程:ZAND渠道出款端到端流程(SP/SQ/VS))
- [[scn_offline_merchant_scan_payment_code]](场景:商户扫用户付款码线下收单(POS / 扫码枪))
- [[scn_online_business_direct_pay]](场景:直连支付 (Direct Pay))
- [[scn_online_business_merchant_async_notify]](场景:商户异步通知接收与重试 (Open API))
- [[scn_online_business_mpgs_channel]](场景:MPGS 渠道卡支付(3DS2 / MOTO / 设备支付 / 卡组织拆分 / 退款Void))
- [[scn_online_business_openapi_protocol_signing]](场景:商户 Open API 接入协议与签名/加密规则)
- [[scn_online_business_payment_code_scan]](场景:付款码被扫线下收单 (POS / 扫码枪))
- [[scn_payment_core_mit_cit_mpgs]](场景:MIT/CIT MPGS 循环（tokenized）支付测试)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp028` · domain=`payment-core`。
