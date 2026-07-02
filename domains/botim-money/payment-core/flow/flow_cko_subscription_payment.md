---
id: flow_cko_subscription_payment
object_type: Flow
name: CKO 渠道订阅支付（签约 + 支付）时序流程
aliases:
- CKO订阅支付
- subscription payment flow
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-25'
source_type: wiki_image
source_ref: wiki_image:bea17c38-8186-48b8-af81-72e06ea7ec56 + wiki_image:85ed1b71-c6cd-4173-8bad-a92dae660154
tags:
- CKO
- 订阅支付
- 签约
- 3DS
- preferSign
- frictionless
related_services:
- svc_cashierii
- svc_authpay
- svc_personal
- svc_member_front
- svc_member
- svc_cmf
- svc_tradeii
related_tables:
- tbl_member_tr_bank_card_token
related_scenarios:
- scn_cko_card_binding_subscription
---

# CKO 渠道订阅支付（签约 + 支付）时序流程

## 概述

CKO 渠道订阅支付的端到端时序，覆盖两条主链：(A) 收银台确认/验证卡支付（preferSign 查询、协议匹配、frictionless 3DS、保存卡 + 下单确认）；(B) 保存卡 + 发起支付返回 3DS 表单、用户验证签约后协议落库并激活卡。下游参与方除已建对象外还涉及 grc（协议/规则中心）、checkout（CKO 渠道侧）、cashdesk（绑卡结果处理），这三者尚无 typed 对象（待补）。

## 步骤(跨系统)

### A. 收银台确认 + 验证卡支付（cgs->cashierii 编排）

**阶段 1：Confirm card payment**
1. `Query auth pay perferSign`：[[svc_cashierii]] → [[svc_authpay]]
2. `Authorize result (perferSign)`：[[svc_authpay]] 返回授权结果与 preferSign
3. `preferSign=Y` 分支：
   - `Query sign protocol list` cashierii → grc（待补：grc 无对象）；`Signed protocols` 返回已签协议
   - `Preroute for card payment channel with signed protocols` cashierii → checkout（待补）；返回 `Protocol whether available (frictionless)`
   - `Payment event with frictionless`：[[svc_cashierii]] → [[svc_authpay]]（authpay 内部 `Save env infor`，回调 `3ds`）
   - `Cache context`：cashierii 内部缓存；`Risk result` 返回 User

**阶段 2：Verify card payment**
4. `Process preferSign and frictionless args`：cashierii 内部处理参数
5. `Save card information with preferSign or frictionless`：[[svc_cashierii]] → [[svc_cmf]]，返回 `Card token id`
6. `Confirm pay`：[[svc_cashierii]] → [[svc_tradeii]]（trade → cmf 回调）

### B. 保存卡 + 签约 + 卡激活

1. `Save card`：User → [[svc_personal]] → [[svc_member_front]]
2. `Save member card` member-front → [[svc_member]]；`Risk Non-Payment event` member-front → grc（待补）
3. `Save card token` member-front → [[svc_cmf]]，返回 `Card token id`
4. `Pay` member-front → [[svc_cmf]] → checkout（待补）`Pay and sign`；返回 `3ds form` 经 member-front → personal → User
5. 用户 `Verify and sign` → checkout（待补）；`Sign protocol data` checkout → [[svc_cmf]]
6. cmf `Save and relate data`（协议落库）→ `Accept bind card result` → cashdesk（待补）
7. cashdesk `Activate card with sign channel` → [[svc_member]]；`Notify grc card success` → grc（待补）

## 关联关系

- **经过的服务（有序，已建对象）**：[[svc_cashierii]] → [[svc_authpay]] → [[svc_personal]] → [[svc_member_front]] → [[svc_member]] → [[svc_cmf]] → [[svc_tradeii]]（= `related_services`）
- **关键表**：[[tbl_member_tr_bank_card_token]]（绑卡签约 token 落库，= `related_tables`）
- **关键场景**：[[scn_cko_card_binding_subscription]]（= `related_scenarios`）
- **未建对象（正文待补）**：grc、checkout、cashdesk

## 校验点

- 阶段 1 中 authpay 返回的 `preferSign=Y` 决定是否进入签约协议匹配分支。
- checkout 返回的 `frictionless` 标识影响 Payment event 与保存卡的处理路径。
- 链 B 保存卡需先在 member 落卡，再上报 grc Risk Non-Payment，随后 cmf 保存 card token；3ds form 经 member-front→personal 透传给 User。
- 用户 Verify and sign 后，checkout 经 `Sign protocol data` 回传 cmf；cmf 须 `Save and relate data`（协议落库 + 关联）。
- cashdesk 必须执行 `Activate card with sign channel`（以签约渠道激活卡）并 `Notify grc card success`。
