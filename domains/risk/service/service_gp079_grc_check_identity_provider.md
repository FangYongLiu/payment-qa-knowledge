---
id: svc_grc_check_identity_provider
object_type: Service
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp079
name: grc-check-identity-provider
dev_owner: Dewen.Li
aliases: [gp079_grc-check-identity-provider]
related_services: [svc_member, svc_kyc, svc_gadget, svc_merchant]
related_tables: []
---

# grc-check-identity-provider

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp079` · domain=`risk`。

## 作用
风控合规身份校验（GRC）—— 被 cashier/cashdesk/cmf/aml 调用做风险事件 / 身份校验

## 系统中的位置
- 功能层:风控 / 合规 / KYC (Risk / Compliance / KYC)
- 业务域:`risk`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 83855 次 · high
- [[svc_kyc]] kyc（实名认证） · 4219 次 · high
- [[svc_gadget]] gadget · 574 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 10 次 · high

**被调用(上游)—— 这些服务调用本服务:**
cashierii, cashdesk-api, cmf, aml, qpay-mpgs, remittance

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_payby_cash_out]](流程:现金提现端到端流程 (Cash Out / Withdraw Cash via POS))
- [[flow_payby_withdraw_to_bank]](流程:提现到银行卡端到端流程 (Transfer to Bank Account / IBAN / Aani))
- [[scn_grc_identity_3ds_rule]](场景:风控核身规则配置控制3DS触发)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp079` · domain=`risk`。
