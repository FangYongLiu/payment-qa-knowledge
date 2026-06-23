---
id: svc_reconciliation
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp043
name: reconciliation
dev_owner: 夏一冰
aliases: [gp043_reconciliation]
related_services: [svc_dpm_manager, svc_member, svc_router, svc_cmf, svc_qpay_zand, svc_pfs_payment, svc_voucher]
related_tables: []
---

# reconciliation

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp043` · domain=`payment-tools`。

## 作用
对账 —— 拉 dpm/member/router/cmf 数据核对

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_dpm_manager]] dpm-manager（账务平台管理） · 10956 次 · high
- [[svc_member]] member（会员 / 账户核心） · 10782 次 · high
- [[svc_router]] router（渠道路由） · 9882 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 9491 次 · high
- [[svc_qpay_zand]] qpay-zand（Zand 银行渠道接入） · 2415 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 57 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 29 次 · high

**被调用(上游)—— 这些服务调用本服务:**
remittance

## 参与的业务场景(cgs 回归)
- §7. 跨境汇款（toC，`test_remittance`）
