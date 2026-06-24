---
id: svc_ccdpm_accounting
object_type: Service
domain: crypto
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp140
name: ccdpm-accounting
dev_owner: Cong.Zhou
aliases: [gp140_ccdpm-accounting]
related_services: []
related_tables: []
---

# ccdpm-accounting

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp140` · domain=`crypto`。

## 作用
加密货币账务记账（CC DPM Accounting，被 member 调用）

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`crypto`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
member

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp140` · domain=`crypto`。
