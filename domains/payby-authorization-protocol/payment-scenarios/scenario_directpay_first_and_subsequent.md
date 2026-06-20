---
id: scn_directpay_first_and_subsequent
object_type: Scenario
domain: payby-authorization-protocol
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/702709784
tags:
- DirectPay
- CardToken
- 3DS
subdomain: payment-scenarios
module: null
sensitivity: normal
name: DirectPay首次与后续支付场景
aliases:
- Direct Pay
- 直连支付
related_services: []
related_tables: []
related_scenarios:
- scn_payandsign_payment
- scn_autodebit_payment
related_logs: []
related_requirements: []
related_failures:
- ts_directpay_3ds_downgrade_token_invalid
---

## 触发/入口
- 用户使用 Direct Pay 直连支付方式发起交易
- 首次支付：用户输入完整卡信息(含CVV)进行支付
- 后续支付：商户使用首次支付返回的 CardToken 发起代扣

## 前置条件
- 首次支付：用户持有可用银行卡
- 后续支付：
  - 已完成首次 Direct Pay 支付且支付成功
  - 商户已通过 notify 方式收到 PayBy 返回的 CardToken
  - 卡处于激活状态(已激活的卡可以用卡id查询出卡信息)
  - 若需走 3DS 认证，卡需为已认证状态(未认证卡可以走3ds认证，认证时需提供cvv)

## 操作步骤
1. 首次支付
   - 用户使用 Direct Pay 提交卡信息完成支付
   - PayBy 存储卡信息，生成 CardToken
   - 支付成功后，PayBy 通过 notify 方式将 CardToken 返回给商户
2. 后续支付(使用已有卡支付)
   - 商户使用已保存的 CardToken 发起支付请求
   - PayBy 根据 CardToken 查询卡信息并完成代扣

## DB 校验点
- 卡激活状态：首次支付成功后卡是否更新为"激活"
- 卡认证状态：是否标记为"已认证"(当前策略：3DS 降级场景下不会更新卡为激活状态)
- CardToken 与卡信息绑定关系是否正确生成

## 预期结果
- 首次支付成功，商户通过 notify 收到 CardToken
- 后续支付可使用 CardToken 完成代扣
- 已知问题：若首次 3DS 支付被降级，卡未激活，导致后续使用 CardToken 无法代扣(详见 [[ts_directpay_3ds_downgrade_token_invalid]])
