---
id: svc_pos_gateway
object_type: Service
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp026
name: pos-gateway
dev_owner: Shuo.Wang
aliases: [gp026_pos-gateway]
related_services: [svc_ues_ws, svc_cashdesk_api]
related_tables: []
---

# pos-gateway

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp026` · domain=`offline-business`。

## 作用
pos-gateway  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`offline-business`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 162 次 · med·待核实
- [[svc_cashdesk_api]] cashdesk-api（统一收银台） · 130 次 · high

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_pos_scan_payment_code]](流程:付款码被 POS 机扫(线下被扫收单)端到端流程)
- [[scn_offline_merchant_scan_payment_code]](场景:商户扫用户付款码线下收单(POS / 扫码枪))
- [[scn_offline_pos_device_types]](场景:POS设备机型能力差异校验)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp026` · domain=`offline-business`。
