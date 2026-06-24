---
id: svc_css
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp096
name: css
dev_owner: Yadong.Lu
aliases: [gp096_css]
related_services: [svc_router]
related_tables: []
---

# css

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp096` · domain=`payment-core`。

## 作用
客服系统（被 fundout 调用，推断）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_router]] router（渠道路由） · 690 次 · high

**被调用(上游)—— 这些服务调用本服务:**
fundout, tradeii

## 参与的业务场景(cgs 回归)
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
