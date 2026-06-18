---
title: CKO渠道订阅支付方案
domain: payby-authorization-protocol
kind: wiki_page
slug: cko-channel-subscription-payment
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:9770c9b6-cd5c-4f9d-ae94-6d4e4b107220
tags: []
---

# CKO渠道订阅支付方案

本页说明 CKO 渠道下订阅支付的需求背景与改造点，包含独立绑卡（CKO121）与收银台卡支付两条主流程。

## 需求背景

- 适用范围：在支付鉴权配置中开启了订阅支付的业务。
- 场景：用户使用已签约的银行卡走 moto 渠道支付时，可路由到 CKO 对应的签约渠道（例如 CKO111）。
- 本质：在原有渠道基础上多出一个 moto 渠道选择。

## 需求拆分

### 1. 独立绑卡（CKO121）

- 绑卡走 CKO121 签约渠道。
- 绑卡成功后，将 CKO 返回的 `signTransactionId` 加密后作为 token 落库到 [[tbl_member_tr_bank_card_token]]。
- 该表中是否存在有效数据，将作为后续支付过程中判断"该卡是否已签约"的依据。
- 详见 [[scn_cko_standalone_card_binding]]。

### 2. 收银台卡支付

- 在收银台进行卡支付时，依据 [[tbl_member_tr_bank_card_token]] 中是否存在该卡的有效签约 token，决定是否走 CKO 签约渠道（如 CKO111）的 moto 流程。

## 测试与参考

- 测试卡号清单见 [[cko-test-cards]]。
- Checkout 官方测试卡文档：https://www.checkout.com/docs/developer-resources/testing/test-cards
- 开发设计：202306-订阅支付
