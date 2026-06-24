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
**UAT Kibana 7d INFO 观测的主要业务类**(app_id=`vis`,=实际在跑的业务操作 / 入口):
- `QueryMigrateTpStaProvider`×57,075 — ZAND 迁移状态查询
- `AbstractMigrateJob`×48,503 — ZAND 迁移任务
- `TransAuditRecordHandlerJob`×46,245 — 流水审计
- `VoucherClientImpl`×52,367 — 调 voucher
- `PfsClientImpl`×48,968 — 调 pfs 清分
- (类名为 Dubbo/RPC 处理器/门面;次数为 7d 调用量级,反映主链路。)
## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`vis`):
- ERROR 98 次,主要:`IBanApplyProcessor`×26
- WARN 18966 次,主要:`TransAuditRecordHandlerJob`×12170、`CompensationEventRepositoryImpl`×4147
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp149` · domain=`payment-core`。
