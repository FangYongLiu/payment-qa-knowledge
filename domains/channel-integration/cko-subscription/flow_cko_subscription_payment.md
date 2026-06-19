---
id: flow_cko_subscription_payment
object_type: Flow
domain: channel-integration
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2228977707
tags:
- cko
- subscription
- sequence
- preferSign
- frictionless
subdomain: cko-subscription
module: null
sensitivity: normal
name: CKO渠道订阅支付时序流程
aliases: []
related_services: []
related_tables:
- tbl_member_tr_bank_card_token
- tbl_member_tr_deduct_channel
- tbl_deduct_t_deduct_protocol
- tbl_protocol_t_contract_sign_info
- tbl_cashdesk_t_filter_node
related_scenarios:
- scn_cko_subscription_test_cards
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

CKO 渠道订阅支付的端到端时序流程，由 User 发起，经 cgs->cashierii 编排，串联 authpay、grc、checkout、cmf、trade 等服务。流程分为两个主阶段：Confirm card payment（确认支付，处理授权、协议查询、预路由与风控）与 Verify card payment（核身验证，保存卡信息并 confirm pay）。

执行顺序：协议查询与预路由在 confirmPayInfo 阶段完成，核身（is3DS）在其后的 verify 阶段产生——先协议与预路由，再核身。

## 步骤(跨系统)

### 1. Confirm card payment (confirmPayInfo 阶段)

- 1.1 Query auth pay perferSign：cgs->cashierii → authpay
- 1.2 Authorize result (perferSign)：authpay → cgs->cashierii
  - 返回 preferSign=Y/N/null；全局配置 alwaysPreferSign=true 且为借记卡时强制 preferSign=Y

当 `preferSign=Y` 时进入签约/订阅分支：

- 1.3 Query sign protocol list：cgs->cashierii → grc（日志：查询卡签约渠道；绑卡场景不查，已存卡查）
- 1.4 Signed protocols：grc → cgs->cashierii
- 1.5 Preroute for card payment channel with signed protocols：cgs->cashierii → checkout（日志：订阅支付渠道预路由）
- 1.6 Protocol whether available (frictionless)：checkout → cgs->cashierii
  - 仅"支持订阅 + 已签约 + 签约渠道可用"时 frictionless=Y
- 1.7 Payment event with frictionless：cgs->cashierii → authpay
  - 1.7.1 Save env info：authpay 自调用
  - 1.7.2 3ds：authpay → cgs->cashierii（GRC 按规则返回是否 3DS）
- 1.8 Cache context：cgs->cashierii 自调用
- 1.9 Risk result：cgs->cashierii → User

### 2. Verify card payment (verify 阶段)

- 2.1 Process preferSign and frictionless args：cgs->cashierii 自调用
  - 未签约且支持订阅 → preferSign=Y
  - 已签约且非 3DS → 传 is3DS（frictionless=Y && is3ds=N 表代扣支付）
- 2.2 Save card information with preferSign or frictionless：cgs->cashierii → cmf
  - 通过 CardTokenCreateRequest 传参；router 按参数过滤路由到签约 3DS 渠道（CKO102）或普通 3DS 渠道（CKO101）或订阅渠道（CKO111）
- 2.3 Card token id：cmf → cgs->cashierii
  - 返回 signTransactionId、signSource=CKO；前端据此认定签约渠道
  - 命中签约渠道时向收银台发绑卡消息，cashier 将 signTransactionId 加密为 token 落到 tr_bank_card_token
- 2.4 Confirm pay：cgs->cashierii → trade
  - 2.4.1 trade → cmf（完成渠道交易并返回结果）

## 涉及服务/表

服务：
- cgs->cashierii：流程编排入口，缓存上下文，处理 preferSign 与 frictionless 参数
- authpay：查询 preferSign、保存环境信息、payment event、3ds 判定
- grc：查询并返回已签署协议列表，按规则返回是否 3DS
- checkout：根据已签协议进行 card payment 渠道预路由，判定 frictionless 是否可用
- cmf：保存卡信息、返回 signTransactionId / signSource / card token id，被 trade 回调完成交易
- trade：执行 confirm pay
- member：作为持久化 lifeline 出现（承载 tr_bank_card_token、tr_deduct_channel）

数据表：
- [[tbl_member_tr_bank_card_token]]：cashier 在签约成功后将 signTransactionId 加密为 token 持久化，channel=签约渠道，状态 Y/N
- [[tbl_member_tr_deduct_channel]]：独立绑卡签约成功后写入
- [[tbl_deduct_t_deduct_protocol]]：PAYANDSIGN 后持久化 deduct_protocol_no
- [[tbl_protocol_t_contract_sign_info]]：sign_contract_no 为契约号
- [[tbl_cashdesk_t_filter_node]]：支付鉴权配置（preferSign）来源

## 校验点

- 1.2 authpay 返回的 preferSign 决定是否进入签约/订阅分支（Y 进入；N/Null 跳过协议查询与预路由，按普通渠道处理）
- 1.4 grc 返回的已签协议列表决定 1.5 预路由的输入；无签约协议时不会命中 CKO111
- 1.6 checkout 返回的 frictionless 标识签约渠道是否可用，仅"支持订阅 + 已签约 + 签约渠道可用"时为 Y
- 1.7.2 is3DS 判定结果决定 verify 阶段路由方向：3DS → CKO102/CKO101；非 3DS（密码/免密） + 已签约 → CKO111
- 2.1 cgs->cashierii 必须先处理 preferSign 与 frictionless 参数后再调用 cmf
- 2.3 cmf 返回的 signTransactionId、signSource=CKO 是判定签约渠道命中的关键字段，并作为 tr_bank_card_token.token 的来源
- 2.2 → 2.4 路径中 router 通过"签约渠道得分高于普通 3DS 渠道 + preferSign/is3DS 过滤"完成最终渠道选择
