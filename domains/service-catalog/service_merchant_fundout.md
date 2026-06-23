---
id: svc_merchant_fundout
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp083
name: merchant-fundout
dev_owner: 王斌
aliases: [gp083_merchant-fundout]
related_services: [svc_fundout, svc_merchant, svc_voucher, svc_member, svc_ppcenter, svc_tradeii, svc_ues_ws]
related_tables: []
---

# merchant-fundout

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp083` · domain=`service-catalog`。

## 作用
商户出款 / 结算代付，调 merchant/fundout(Fos)/voucher/ppcenter

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_fundout]] fundout（出款 / 代付核心） · 1825 次 · med·待核实
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 246 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 218 次 · high
- [[svc_member]] member（会员 / 账户核心） · 108 次 · high
- [[svc_ppcenter]] ppcenter（产品中心） · 80 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 24 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 14 次 · med·待核实
