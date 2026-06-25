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

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_acquire_product_application]](流程:收单商户控台产品申请与开通流程)
- [[flow_device_activation]](流程:设备激活端到端流程(Smart POS))
- [[flow_merchant_onboarding]](流程:商户注册与入驻端到端流程(Acquire + WPS))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp161` · domain=`portal-operations`。
