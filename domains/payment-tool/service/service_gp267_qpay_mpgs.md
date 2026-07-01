---
id: svc_qpay_mpgs
object_type: Service
domain: payment-tool
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp267
name: qpay-mpgs
aliases: [gp267_qpay-mpgs]
related_services: [svc_onboarding, svc_cards, svc_grc_check_identity_provider, svc_ues_ws]
related_tables: []
---

# qpay-mpgs

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp267` · domain=`channel`。

## 作用
Mastercard Payment Gateway（MPGS）渠道接入，3DS2 卡支付

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`channel`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_onboarding]] onboarding（商户 / 用户入网） · 21348 次 · high
- [[svc_cards]] cards（卡管理） · 2356 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 1762 次 · med·待核实
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 6 次 · med·待核实

## 参与的业务场景(cgs 回归)
- §4. 卡渠道入金 3DS（`test_mpgs_fundIn` / `test_cko_fundIn`）

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[scn_mpgs_onboarding]](场景:MPGS Onboarding 组件架构与数据模型)
- [[scn_online_business_mpgs_channel]](场景:MPGS 渠道卡支付(3DS2 / MOTO / 设备支付 / 卡组织拆分 / 退款Void))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp267` · domain=`channel`。
