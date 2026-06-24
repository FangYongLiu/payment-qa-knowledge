---
id: svc_customer_frontend
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp064
name: customer-frontend
dev_owner: Sijia.Zhang
aliases: [gp064_customer-frontend]
related_services: [svc_merchant, svc_acquireii, svc_voucher, svc_invoice, svc_protocol, svc_member, svc_cc_deposit, svc_kyc, svc_cc_transfer]
related_tables: []
---

# customer-frontend

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp064` · domain=`online-business`。

## 作用
C 端用户前端 BFF

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`online-business`

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

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp064` · domain=`online-business`。
