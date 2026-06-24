---
id: svc_voucher
object_type: Service
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp009
name: voucher
dev_owner: Dewen.Li
aliases: [gp009_voucher]
related_services: []
related_tables: []
---

# voucher

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp009` · domain=`risk`。

## 作用
全局 ID 与幂等凭证（getGlobalId / recordReqVoucher）—— 被交易 / 收单 / 出款广泛调用的基础设施

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`risk`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
tradeii, vis, offline-payment, acquireii, escrow, merchant-fundout

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §7. 跨境汇款（toC，`test_remittance`）
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）

## 观测到的对外方法
getGlobalId, recordReqVoucher
