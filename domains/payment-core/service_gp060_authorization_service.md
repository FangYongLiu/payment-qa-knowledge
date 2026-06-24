---
id: svc_authorization_service
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp060
name: authorization-service
dev_owner: Yadong.Lu
aliases: [gp060_authorization-service]
related_services: []
related_tables: []
---

# authorization-service

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp060` · domain=`payment-core`。

## 作用
授权服务（授权 token / 权限，推断）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`payment-core`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
merchant

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`authorization-service`):
- ERROR 3 次(均为基础设施健康检查噪声,无显著业务错误)
- WARN 3 次(均为基础设施噪声)
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp060` · domain=`payment-core`。
