---
id: svc_escrow
object_type: Service
domain: payment-core
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp104
name: escrow
dev_owner: Qian.Wang
aliases: [gp104_escrow]
related_services: [svc_ufs2, svc_deposit, svc_voucher, svc_ues_ws, svc_query, svc_member, svc_cms, svc_grc_check_identity_provider]
related_tables: []
---

# escrow

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp104` · domain=`service-catalog`。

## 作用
担保 / 托管交易（推断：调 deposit/voucher/ues）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ufs2]] ufs2（用户文件 / 数据服务） · 72171 次 · med·待核实
- [[svc_deposit]] deposit（充值 / 存款服务） · 35105 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 28092 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 24604 次 · med·待核实
- [[svc_query]] query（查询 / 报表服务） · 927 次 · high
- [[svc_member]] member（会员 / 账户核心） · 152 次 · high
- [[svc_cms]] cms（内容 / 配置管理） · 42 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 4 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
cmf, counter
