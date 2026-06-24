---
id: svc_pcm
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp046
name: pcm
dev_owner: Yu.Tang
aliases: [gp046_pcm]
related_services: [svc_pcs, svc_ues_ws]
related_tables: []
---

# pcm

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp046` · domain=`payment-core`。

## 作用
pcm  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_pcs]] pcs · 178 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 162 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
cashdesk-api

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
**UAT Kibana 7d INFO 观测的主要业务类**(app_id=`pcm`,=实际在跑的业务操作 / 入口):
- `PayCodeImprintJob`×6,051 — 付款码压印任务
- (类名为 Dubbo/RPC 处理器/门面;次数为 7d 调用量级,反映主链路。)
## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`pcm`):
- ERROR 12 次(均为基础设施健康检查噪声,无显著业务错误)
- WARN 7 次(均为基础设施噪声)
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp046` · domain=`payment-core`。
