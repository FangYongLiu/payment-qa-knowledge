---
id: svc_rdgs
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp216
name: rdgs
dev_owner: Yongxing.Cao
aliases: [gp216_rdgs]
related_services: [svc_query, svc_ufs2]
related_tables: []
---

# rdgs

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp216` · domain=`payment-core`。

## 作用
报表 / 数据服务（调 query/ufs）

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_query]] query（查询 / 报表服务） · 2583 次 · high
- [[svc_ufs2]] ufs2（用户文件 / 数据服务） · 1097 次 · med·待核实

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`rdgs`):
- ERROR 8396 次,主要:`ReportTaskDetailJob`×3269、`RevaluationReportDetailTaskImpl`×3017
- WARN 5044 次,主要:`ReportScheduleJob`×5040
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp216` · domain=`payment-core`。
