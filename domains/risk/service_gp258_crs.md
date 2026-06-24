---
id: svc_crs
object_type: Service
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp258
name: crs
dev_owner: Yu.Tang,Xiaoyu.Sun
aliases: [gp258_crs]
related_services: [svc_voucher, svc_member, svc_pfs_payment]
related_tables: []
---

# crs

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp258` · domain=`risk`。

## 作用
（推断：客户 / 风控相关，调 member/voucher）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`risk`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 2104 次 · high
- [[svc_member]] member（会员 / 账户核心） · 2082 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 1231 次 · high

**被调用(上游)—— 这些服务调用本服务:**
ppc
