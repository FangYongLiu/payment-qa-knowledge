---
id: svc_vis
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp149
name: vis
dev_owner: 王迁
aliases: [gp149_vis]
related_services: [svc_voucher, svc_pfs_payment, svc_deposit]
related_tables: []
---

# vis

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp149` · domain=`service-catalog`。

## 作用
（推断：虚拟账户 / 收款，调 voucher/pfs/deposit）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 669 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 620 次 · high
- [[svc_deposit]] deposit（充值 / 存款服务） · 160 次 · high

**被调用(上游)—— 这些服务调用本服务:**
fundout

## 参与的业务场景(cgs 回归)
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）
