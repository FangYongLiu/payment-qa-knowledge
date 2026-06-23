---
id: svc_fundout
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp012
name: fundout
aliases: [gp012_fundout]
related_services: [svc_member, svc_pbs, svc_pfs_payment, svc_css, svc_acs, svc_vis, svc_merchant, svc_voucher, svc_cards, svc_exchange, svc_cashierii, svc_ues_ws, svc_cmf]
related_tables: []
---

# fundout

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp012` · domain=`online-business`。

## 作用
出款 / 代付核心 —— 编排 member/pbs/acs/css/vis/cards/merchant/voucher

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`online-business`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 38415 次 · high
- [[svc_pbs]] pbs（计费 / 定价） · 34971 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 16376 次 · high
- [[svc_css]] css（客服系统） · 11756 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 11750 次 · high
- [[svc_vis]] vis · 10580 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 5130 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 5052 次 · high
- [[svc_cards]] cards（卡管理） · 1892 次 · high
- [[svc_exchange]] exchange（换汇 / 汇率服务） · 982 次 · high
- [[svc_cashierii]] cashierii（收银核心） · 826 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 303 次 · med·待核实
- [[svc_cmf]] cmf（渠道管理与资金） · 38 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant-fundout, merchant-frontend, personal, cashdesk-api

## 参与的业务场景(cgs 回归)
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §6. 提现（toC，`test_withdraw`）

## 观测到的对外方法
createInnerFundout, createInnerFundoutV2
