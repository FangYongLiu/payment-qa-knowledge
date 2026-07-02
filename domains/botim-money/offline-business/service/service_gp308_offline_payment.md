---
id: svc_offline_payment
object_type: Service
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp308
name: offline-payment
aliases: [gp308_offline-payment]
related_services: [svc_pfs_payment, svc_ues_ws, svc_css, svc_member, svc_authpay, svc_voucher]
related_tables: []
---

# offline-payment

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp308` · domain=`offline-business`。

## 作用
线下支付（扫码 / POS 收款），编排 pfs/member/voucher/pbs

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`offline-business`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 6022948 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 298962 次 · med·待核实
- [[svc_css]] css（客服系统） · 164052 次 · high
- [[svc_member]] member（会员 / 账户核心） · 75504 次 · high
- [[svc_authpay]] authpay（授权支付 / 免密代扣执行） · 54692 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 47002 次 · high

**被调用(上游)—— 这些服务调用本服务:**
acquireii

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[scn_offline_pos_device_types]](场景:POS设备机型能力差异校验)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp308` · domain=`offline-business`。
