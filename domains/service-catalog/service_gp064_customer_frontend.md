---
id: svc_customer_frontend
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp064
name: customer-frontend
dev_owner: 王斌
aliases: [gp064_customer-frontend]
related_services: [svc_merchant, svc_acquireii, svc_voucher, svc_invoice, svc_protocol, svc_member, svc_cc_deposit, svc_kyc, svc_cc_transfer]
related_tables: []
---

# customer-frontend

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp064` · domain=`service-catalog`。

## 作用
C 端用户前端 BFF

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 6684 次 · high
- [[svc_acquireii]] acquireii（收单核心） · 1542 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 1542 次 · high
- [[svc_invoice]] invoice · 318 次 · high
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 216 次 · high
- [[svc_member]] member（会员 / 账户核心） · 102 次 · high
- [[svc_cc_deposit]] cc-deposit（加密货币充值） · 12 次 · high
- [[svc_kyc]] kyc（实名认证） · 12 次 · high
- [[svc_cc_transfer]] cc-transfer · 9 次 · high
