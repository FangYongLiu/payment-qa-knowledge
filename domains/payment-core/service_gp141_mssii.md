---
id: svc_mssii
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp141
name: mssii
dev_owner: Yadong.Lu
aliases: [gp141_mssii]
related_services: [svc_merchant, svc_member, svc_kyc]
related_tables: []
---

# mssii

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp141` · domain=`payment-core`。

## 作用
营销 / 商户消息服务（推断：调 merchant/member）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 4366 次 · high
- [[svc_member]] member（会员 / 账户核心） · 2918 次 · high
- [[svc_kyc]] kyc（实名认证） · 1598 次 · high

**被调用(上游)—— 这些服务调用本服务:**
marketing-event

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`mssii`):
- ERROR 5 次,主要:`CashierActivityProcessor`×5
- WARN 1005 次,主要:`QueryInterestsServiceImpl`×388、`ResponseUtil`×303
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp141` · domain=`payment-core`。
