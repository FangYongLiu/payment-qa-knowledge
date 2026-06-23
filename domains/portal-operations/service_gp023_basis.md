---
id: svc_basis
object_type: Service
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp023
name: basis
dev_owner: 夏一冰
aliases: [gp023_basis]
related_services: [svc_kyc_service, svc_ufs2, svc_member, svc_merchant, svc_tradeii]
related_tables: []
---

# basis

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp023` · domain=`portal-operations`。

## 作用
基础数据(Basis)  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`portal-operations`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_kyc_service]] kyc-service（实名认证服务） · 17250 次 · high
- [[svc_ufs2]] ufs2（用户文件 / 数据服务） · 14895 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 13779 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 232 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 6 次 · high
