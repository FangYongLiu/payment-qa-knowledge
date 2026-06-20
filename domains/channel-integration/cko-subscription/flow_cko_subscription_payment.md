---
id: flow_cko_subscription_payment
object_type: Flow
domain: channel-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:5b35d40b-b532-44de-b69e-abffc289be85
tags:
- CKO
- subscription
- preferSign
- frictionless
- confirmPayInfo
- verify
subdomain: cko-subscription
module: null
sensitivity: normal
name: CKO渠道订阅支付端到端流程
aliases: []
related_services: []
related_tables:
- tr_bank_card_token
- tr_bank_account
- tr_deduct_channel
- t_deduct_protocol
- t_contract_sign_info
- tt_inst_order
- tt_inst_result
- t_filter_node
related_scenarios:
- scn_cko_subscription_payment_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

CKO渠道订阅支付的端到端时序流程，由 User 发起，经 cgs->cashierii 编排，串联 authpay、grc、checkout、cmf、trade 等服务。流程聚焦补充签约支付与代扣支付的路由决策，分为两个主阶段：Confirm card payment（确认支付，处理鉴权 preferSign、协议查询、预路由与风控）与 Verify card payment（核身与卡信息保存、确认支付）。协议查询与预路由在 confirmPayInfo 阶段完成，核身（is3DS）在其后的 verify 阶段产生——先协议与预路由，再核身。

## 步骤(跨系统)

### 阶段一：Confirm card payment (User → cgs->cashierii)（对应 /cashdesk/confirmPayInfo）

- 1.1 Query auth pay perferSign：cgs->cashierii → authpay
- 1.2 Authorize result (perferSign)：authpay → cgs->cashierii
  - authpay 按商户组、产品码、支付场景、入口、版本号返回鉴权结果，携带 preferSign（Y / N / null）
  - 全局配置（2023-8）：alwaysPreferSign=true 且为借记卡时，强制 preferSign=Y（cashdesk-api.yml→cashdesk.alwaysPreferSign；gp193_cashierii.yml→cashier.alwaysPreferSign）

当 `preferSign=Y` 时进入以下分支（已存卡查询，绑卡场景不查）：

- 1.3 Query sign protocol list：cgs->cashierii → grc（日志：查询卡签约渠道）
- 1.4 Signed protocols：grc → cgs->cashierii
- 1.5 Preroute for card payment channel with signed protocols：cgs->cashierii → checkout（日志：订阅支付渠道预路由）
- 1.6 Protocol whether available (frictionless)：checkout → cgs->cashierii
  - 仅当「支持订阅 + 已签约 + 签约渠道可用」时 frictionless=Y
- 1.7 Payment event with frictionless：cgs->cashierii → authpay
  - 1.7.1 Save env infor：authpay 自调用
  - 1.7.2 3ds：authpay → cgs->cashierii（按规则返回是否 3DS）
- 1.8 Cache context：cgs->cashierii 自调用
- 1.9 Risk result：cgs->cashierii → User

### 阶段二：Verify card payment (User → cgs->cashierii)（对应 /cashdesk/verify）

- 2.1 Process preferSign and frictionless args：cgs->cashierii 自调用
  - 未签约且支持订阅 → preferSign=Y
  - 已签约且非 3DS → frictionless=Y && is3ds=N（代扣 / 订阅）
- 2.2 Save card information with preferSign or frictionless：cgs->cashierii → cmf（CardTokenCreateRequest）
  - router 按「渠道得分 + 扩展参数匹配」过滤签约 3DS 渠道或普通 3DS 渠道
- 2.3 Card token id：cmf → cgs->cashierii
  - 命中签约渠道时返回 signTransactionId、signSource=CKO，前端据此认定签约渠道；收银台将签约信息存入 member（tr_bank_card_token，signTransactionId 加密为 token）
- 2.4 Confirm pay：cgs->cashierii → trade
  - 2.4.1 trade → cmf

### 路由结果（端到端落地渠道）

- preferSign=Y & is3DS=Y & 签约渠道可用 → CKO102（签约）；不可用降级 CKO101（不签约）
- preferSign=Y & 非 3DS（密码/免密）& 已签约 & 渠道可用 → CKO111（订阅/代扣，frictionless=Y）
- preferSign=N / Null → 普通 3DS 渠道 CKO101，不签约不订阅
- 独立绑卡：固定 CKO121，不受配置影响

## 涉及服务/表

服务：
- cgs->cashierii：流程编排入口，缓存上下文，处理 preferSign 与 frictionless 参数
- authpay：查询 preferSign、保存环境信息、3ds 判定、支付事件处理
- grc：查询并返回已签署协议列表（GRC 支付事件 frictionless=null/Y；按规则返回是否 3DS）
- checkout：基于已签协议执行 card payment 渠道预路由，判定 frictionless 是否可用；router 完成最终渠道过滤
- cmf：保存卡信息、返回 card token id（含 signTransactionId / signSource），并被 trade 回调
- trade：执行 confirm pay
- member：承载卡与协议数据（lifeline）

表：
- tr_bank_account（member）：银行卡账户，status / 鉴权状态
- tr_bank_card_token（member）：卡协议 token 核心表，channel=签约渠道，token=加密签约号，status Y/N
- tr_deduct_channel（member）：独立绑卡签约成功后写入
- t_deduct_protocol（deduct）：PAYANDSIGN 后落库，deduct_protocol_no 用于代扣
- t_contract_sign_info（protocol）：sign_contract_no 即合约号
- tt_inst_order / tt_inst_result（cmf）：渠道指令订单与结果，扩展字段存渠道返回
- t_filter_node（cashdesk）：支付鉴权配置（preferSign），unit_id=13 已存卡 / 4 新卡

## 校验点

- 1.2 authpay 返回的 preferSign（Y/N/null）决定是否进入签约分支；同时校验全局 alwaysPreferSign 对借记卡的覆盖逻辑
- 1.3–1.4 协议查询日志「查询卡签约渠道」是否按 preferSign + 卡场景正确触发（绑卡不查、已存卡查）
- 1.5–1.6 预路由日志「订阅支付渠道预路由」是否产生；checkout 返回 frictionless 仅在「支持订阅 + 已签约 + 签约渠道可用」时为 Y
- 1.7 风控支付事件传 frictionless 是否与预路由结果一致
- 2.1 verify 阶段对 preferSign 与 frictionless 的组合处理：仅「支持订阅 + 已签约 + 签约渠道可用 + 核身非 3DS」时 frictionless=Y
- 2.2–2.3 CardTokenCreateRequest 落到 cmf
