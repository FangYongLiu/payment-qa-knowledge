---
id: svc_npss_gateway
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp210
name: npss-gateway
dev_owner: Qian.Wang
aliases: [gp210_npss-gateway]
related_services: [svc_npss]
related_tables: []
---

# npss-gateway

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp210` · domain=`payment-core`。

## 作用
NPSS（即时支付系统）报文网关

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_npss]] npss（即时支付 / 账单） · 17610 次 · high

**被调用(上游)—— 这些服务调用本服务:**
npss, qpay-npss

## 参与的业务场景(cgs 回归)
- §8. 账单 / 即时支付（`test_ppcTransaction`，NPSS）

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`npss-gateway`):
- ERROR 26 次(均为基础设施健康检查噪声,无显著业务错误)
- WARN 40 次(均为基础设施噪声)
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp210` · domain=`payment-core`。
