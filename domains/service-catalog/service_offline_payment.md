---
id: svc_offline_payment
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp308
name: offline-payment
aliases: [gp308_offline-payment]
related_services: [svc_pfs_payment, svc_member, svc_voucher, svc_pbs]
related_tables: []
---

# offline-payment

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp308` · domain=`service-catalog`。

## 作用
线下支付（扫码 / POS 收款），编排 pfs/member/voucher/pbs

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 13546 次 · high
- [[svc_member]] member（会员 / 账户核心） · 1304 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 648 次 · high
- [[svc_pbs]] pbs（计费 / 定价） · 339 次 · high
