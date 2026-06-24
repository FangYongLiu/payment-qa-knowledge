---
id: svc_basis_merchant
object_type: Service
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp161
name: basis-merchant
dev_owner: Chahid
aliases: [gp161_basis-merchant]
related_services: [svc_member, svc_merchant, svc_device, svc_statementii, svc_onboarding, svc_aml, svc_cashierii]
related_tables: []
---

# basis-merchant

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp161` · domain=`portal-operations`。

## 作用
基础数据(Basis)（merchant）  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`portal-operations`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 20751 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 14217 次 · high
- [[svc_device]] device（设备 / 产品中心接入） · 4887 次 · high
- [[svc_statementii]] statementii（账单 / 对账单） · 384 次 · high
- [[svc_onboarding]] onboarding（商户 / 用户入网） · 330 次 · high
- [[svc_aml]] aml（反洗钱） · 134 次 · high
- [[svc_cashierii]] cashierii（收银核心） · 12 次 · high
