---
id: domain_offline_business
object_type: Domain
name: offline-business
aliases: [线下业务]
domain: offline-business
business_line: botim-money
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [offline-business, 线下业务]
related_services: [svc_pos_gateway, svc_device, svc_iso8583_gateway, svc_offline_payment]
---

# offline-business(线下业务)

> 业务域总览(入口节点)。owner xiaoqian.wei,wanmei.ding。细节见各服务对象。

## 概述
线下业务域:POS 收单网关、设备管理、线下支付、ISO8583 网关等线下受理能力。

## 覆盖范围
共 4 个服务:pos-gateway、device、iso8583-gateway、offline-payment。

## QA 关注点
- 待补。

## 流程 / 场景 / 排障 索引
本域 流程 / 场景 / 排障 / 自动化 对象索引:
- [[flow_device_activation]](流程:设备激活端到端流程(Smart POS))
- [[scn_offline_merchant_scan_payment_code]](场景:商户扫用户付款码线下收单(POS / 扫码枪))
- [[scn_offline_pos_device_types]](场景:POS设备机型能力差异校验)
- [[scn_pos_transaction_db_check]](场景:POS刷卡交易落库检查)

## 服务 / 参考索引(补)
- [[svc_kiosk_mgmt]](KIOSK 管理)· [[reference_offline_business_overview]](线下业务总览)
