---
id: svc_reconciliation
object_type: Service
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp043
name: reconciliation
dev_owner: Yibing.Xia
aliases: [gp043_reconciliation]
related_services: [svc_dpm_manager, svc_member, svc_router, svc_cmf, svc_qpay_zand, svc_vis, svc_pfs_payment, svc_voucher]
related_tables: []
---

# reconciliation

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp043` · domain=`payment-core`。

## 作用
对账 —— 拉 dpm/member/router/cmf 数据核对

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_dpm_manager]] dpm-manager（账务平台管理） · 4437599 次 · high
- [[svc_member]] member（会员 / 账户核心） · 4408030 次 · high
- [[svc_router]] router（渠道路由） · 2008999 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 1865107 次 · high
- [[svc_qpay_zand]] qpay-zand（Zand 银行渠道接入） · 919811 次 · high
- [[svc_vis]] vis · 12336 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 8125 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 4958 次 · high

**被调用(上游)—— 这些服务调用本服务:**
remittance

## 参与的业务场景(cgs 回归)
- §7. 跨境汇款（toC，`test_remittance`）

## 涉及的 API / 数据库表
- **暴露/相关 API**:MQ `FundFlowHandler`(收资金流消息);`Reconciliation=>Router calcFee`(算费)、`reconciliation=>cmf getInstOrder`(取机构订单)。
- **读写的表**:入账流水 / 清算流水 / 对账汇总(具体对象待补)。

## 关键方法 / 入口(UAT 实测 + 商户端2025)
- **收资金流**:支付/入账完成后 `FundFlowHandler 收到消息`(含 accountDate/amount/bizNo/clearingOrderId/fundsChannel/paymentSeqNo/productCode),据此建入账流水。
- **算费/取单**:`Reconciliation=>Router calcFee request`(交易费用计算)、`reconciliation=>cmf getInstOrder result`(取机构订单核对)。

## 对账 / 结转业务(商户端2025)
- **两类流水**:入账流水(来自 PayBy 已支付完成订单)vs 清算流水(来自渠道商对账单)。
- **对账汇总**:自动/手动下载渠道对账文件 → 解析 → 入账流水与清算流水**逐笔比对**(金额/状态/单号)。
- **结转**:对平后结转到渠道商 PayBy **待结算账户 → 基本账户**。
- 渠道对账单下载配置:HTTP / SFTP + 解析脚本(见清算后台 [[svc_counter]] 配置)。

## 测试要点 / 排障 / 常见问题(UAT 实测)
- **对账差异**:清算文件有交易但系统流水为 `process` → 对账失败 → 人工确认(见 [[ts_fundout_stuck_in_process]]);金额/单号不匹配为典型差异。
- **怎么测/定位**:按 `paymentSeqNo`/`clearingOrderId` 跟 FundFlow 入账流水;造渠道对账单与入账流水的匹配/差异用例。
- 费用核对:reconciliation calcFee 与 [[svc_pbs]] 算费、`t_payment_info` 费用式(pf_vat/pfbt)一致。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp043` · domain=`payment-core`。
