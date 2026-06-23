---
id: svc_deposit
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp011
name: deposit
aliases: [gp011_deposit]
related_services: []
related_tables: []
---

# deposit

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp011` · domain=`service-catalog`。

## 作用
充值 / 存款服务（被 escrow/vis 调用，推断）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`service-catalog`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
escrow, vis

## 参与的业务场景(cgs 回归)
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）
