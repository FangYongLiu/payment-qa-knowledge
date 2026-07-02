---
id: svc_pts
object_type: Service
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp040
name: pts
dev_owner: Guoyou.Ma
aliases: [gp040_pts]
related_services: []
related_tables: []
---

# pts

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp040` · domain=`payment-tools`。

## 作用
（推断：支付 token / 会话服务，被 personal 调用）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`payment-tools`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
personal

## 参与的业务场景(cgs 回归)
- §6. 提现（toC，`test_withdraw`）

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp040` · domain=`payment-tools`。
