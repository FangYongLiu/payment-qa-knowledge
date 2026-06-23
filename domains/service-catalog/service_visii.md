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
related_services: [svc_member, svc_qpay_fts, svc_grc_check_identity_provider, svc_voucher, svc_pns, svc_deposit, svc_cards, svc_fundout, svc_reconciliation, svc_pfs_payment]
related_tables: []
---

# visii

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp317` · domain=`service-catalog`。

## 作用
（推断：虚拟账户 / 收款 II，调 fts/member）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 366059 次 · high
- [[svc_qpay_fts]] qpay-fts（FTS 渠道接入） · 77735 次 · med·待核实
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 11154 次 · med·待核实
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 7716 次 · high
- [[svc_pns]] pns（支付通知服务） · 3843 次 · high
- [[svc_deposit]] deposit（充值 / 存款服务） · 3712 次 · high
- [[svc_cards]] cards（卡管理） · 2649 次 · high
- [[svc_fundout]] fundout（出款 / 代付核心） · 1342 次 · high
- [[svc_reconciliation]] reconciliation（对账） · 1161 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 442 次 · high

**被调用(上游)—— 这些服务调用本服务:**
counter, fcw, npss

## 参与的业务场景(cgs 回归)
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）
