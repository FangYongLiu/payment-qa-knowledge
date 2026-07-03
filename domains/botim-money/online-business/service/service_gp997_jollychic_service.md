---
id: svc_jollychic_service
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp997
name: jollychic-service
dev_owner: Sijia.Zhang
aliases: [gp997_jollychic-service]
related_services: [svc_acquireii]
related_tables: []
---

# jollychic-service

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp997` · domain=`online-business`。

## 作用
jollychic-service  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`online-business`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_acquireii]] acquireii（收单核心） · 6 次 · high

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp997` · domain=`online-business`。

## 涉及的表(DB)
本服务读写 `jollychic` 库(2 张,见 `online-business/table/jollychic/`)。主要表:[[tbl_jollychic_t_acquire_order]]。
