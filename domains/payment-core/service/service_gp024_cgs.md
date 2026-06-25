---
id: svc_cgs
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp024
name: cgs
dev_owner: Yongxing.Cao
aliases: [gp024_cgs]
related_services: []
related_tables: []
---

# cgs

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp024` · domain=`payment-core`。

## 作用
(本窗口未观测到该服务的运行时活动,作用待业务补充。)

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
(本窗口未观测到与其它服务的调用关系)

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_add_funds_via_bank_card]](流程:银行卡充值(Add Funds via Bank Card)端到端流程)
- [[flow_botim_transfer]](流程:BOTIM/ToC 转账与加款端到端流程)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_h5_jsbridge_auth]](流程:H5 客户端 jsBridge 鉴权流程(Verifier Token + Session))
- [[flow_payby_cash_out]](流程:现金提现端到端流程 (Cash Out / Withdraw Cash via POS))
- [[flow_payby_withdraw_to_bank]](流程:提现到银行卡端到端流程 (Transfer to Bank Account / IBAN / Aani))
- [[flow_ppc_card_lifecycle]](流程:PPC 卡端到端业务流程(开卡→激活→交易→清算→关卡))
- [[flow_remittance_pix_mpc]](流程:PIX MPC 商户呈现码扫码支付端到端流程)
- [[flow_wallet_send_money]](流程:Wallet Send Money 转账(KYC结算 / 过期退款))
- [[scn_wallet_withdraw_to_bank]](场景:提现到银行卡场景 (Transfer to Bank Account 字段/状态/限额/测试))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp024` · domain=`payment-core`。
