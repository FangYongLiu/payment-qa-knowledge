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
related_services: [svc_member, svc_pbs, svc_pfs_payment, svc_acs, svc_css, svc_vis, svc_merchant, svc_voucher, svc_cards, svc_exchange]
related_tables: []
---

# fundout

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp012` · domain=`online-business`。

## 作用
出款 / 代付核心 —— 编排 member/pbs/acs/css/vis/cards/merchant/voucher

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`online-business`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_member]] member（会员 / 账户核心） · 760 次 · high
- [[svc_pbs]] pbs（计费 / 定价） · 474 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 328 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 236 次 · high
- [[svc_css]] css（客服系统） · 236 次 · high
- [[svc_vis]] vis · 216 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 112 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 110 次 · high
- [[svc_cards]] cards（卡管理） · 42 次 · high
- [[svc_exchange]] exchange（换汇 / 汇率服务） · 24 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant-fundout, merchant-frontend, personal, cashdesk-api

## 参与的业务场景(cgs 回归)
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §6. 提现（toC，`test_withdraw`）

## 观测到的对外方法
createInnerFundout, createInnerFundoutV2
