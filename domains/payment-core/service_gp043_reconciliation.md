---
id: svc_reconciliation
object_type: Service
domain: payment-core
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
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`reconciliation`):
- ERROR 910372 次,主要:`crowAdjustStrategyZandRpsEscrowProcessor`×583526、`RouteSftpMethodProcessor`×217139
- WARN 1915798 次,主要:`BalanceMonitorServiceImpl`×1707046
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp043` · domain=`payment-core`。
