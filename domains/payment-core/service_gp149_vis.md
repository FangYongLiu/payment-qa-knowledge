---
id: svc_vis
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp149
name: vis
dev_owner: Qian.Wang
aliases: [gp149_vis]
related_services: [svc_voucher, svc_pfs_payment, svc_grc_check_identity_provider, svc_query, svc_deposit, svc_pns, svc_member, svc_reconciliation, svc_qpay_fts]
related_tables: []
---

# vis

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp149` · domain=`payment-core`。

## 作用
（推断：虚拟账户 / 收款，调 voucher/pfs/deposit）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 121081 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 114156 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 69036 次 · med·待核实
- [[svc_query]] query（查询 / 报表服务） · 69028 次 · high
- [[svc_deposit]] deposit（充值 / 存款服务） · 29218 次 · high
- [[svc_pns]] pns（支付通知服务） · 5346 次 · high
- [[svc_member]] member（会员 / 账户核心） · 2374 次 · high
- [[svc_reconciliation]] reconciliation（对账） · 48 次 · high
- [[svc_qpay_fts]] qpay-fts（FTS 渠道接入） · 36 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
fundout

## 涉及的 API / 数据库表
**读写的表:** [[tbl_vis_t_virtual_account]] vis.t_virtual_account 虚拟账户表、[[tbl_vis_t_notify_transaction_flow]] vis.t_notify_transaction_flow 交易通知流水表

## 参与的业务场景(cgs 回归)
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_wallet_vis_iban_retry_job]](自动化:vis_ibanAccountRetryJob 批次处理任务 (VAM IBAN 申请重试 Job))
- [[flow_merchant_onboarding]](流程:商户注册与入驻端到端流程(Acquire + WPS))
- [[scn_wallet_vam_iban_apply_activate]](场景:VAM IBAN 虚拟账户申请激活与交易通知 (VAM IBAN Apply / Activate / Notify))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp149` · domain=`payment-core`。
