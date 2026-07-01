---
id: svc_botim_credit
object_type: Service
domain: lending
status: draft
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-06-24'
source_type: callgraph_observed
source_ref: SERVICE_CALLGRAPH_UAT_20260623.md
tags: []
name: botim-credit
dev_owner: Xiaopei.Yan
aliases: [botim-credit]
related_services: [svc_member, svc_pns]
related_tables: []
---

# botim-credit

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`` · domain=`quantix`。

## 作用
botim-credit  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`quantix`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 4818 次 · med·待核实
- [[svc_pns]] pns（支付通知服务） · 2426 次 · high

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`` · domain=`quantix`。
