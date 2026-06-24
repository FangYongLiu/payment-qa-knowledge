---
id: svc_marketing
object_type: Service
domain: marketing
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp068
name: marketing
dev_owner: Yadong.Lu
aliases: [gp068_marketing]
related_services: []
related_tables: []
---

# marketing

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp068` · domain=`marketing`。

## 作用
营销服务（优惠 / 活动，被 acquire/cashdesk 调用）

## 系统中的位置
- 功能层:营销 / 产品 / 报价 (Marketing / Product / Quote)
- 业务域:`marketing`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
acquireii, cashdesk-api

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp068` · domain=`marketing`。
