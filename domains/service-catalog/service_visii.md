---
id: svc_visii
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp317
name: visii
aliases: [gp317_visii]
related_services: [svc_qpay_fts, svc_member]
related_tables: []
---

# visii

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp317` · domain=`service-catalog`。

## 作用
（推断：虚拟账户 / 收款 II，调 fts/member）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_qpay_fts]] qpay-fts（FTS 渠道接入） · 682 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 262 次 · high

## 参与的业务场景(cgs 回归)
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）
