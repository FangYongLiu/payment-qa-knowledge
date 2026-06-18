---
title: CKO Channel订阅支付
domain: payby-authorization-protocol
kind: wiki_page
slug: cko-channel-subscription-payment
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/1082523699
tags: []
---

# CKO Channel订阅支付

本页梳理 CKO 渠道接入订阅支付（Subscription Payment）的需求背景、需求拆分以及测试卡信息。

## 需求背景

- 针对指定业务（支付鉴权配置支持订阅支付的业务），当用户使用 **已签约的银行卡** 走 moto 渠道场景时，可走 CKO 对应的签约渠道（如 CKO111）。
- 可理解为：在原有渠道基础上多一个 moto 渠道。

## 需求拆分

### 1. 独立绑卡：CKO121

- 绑卡走 CKO121 签约渠道。
- 成功后落库到 `member.tr_bank_card_token`：
  - 落库内容：CKO 返回字段 `signTransactionId`，加密后作为 token 存储。
- 后续支付时，通过该表是否存在有效数据，判断该卡是否已签约。

### 2. 收银台卡支付

- 收银台场景下使用已签约卡完成支付，走 CKO 对应签约渠道。

## 测试卡信息

| Card No | Description |
| --- | --- |
| 4010 0617 0000 0021 | 本地卡 - Debit |
| 5385 3083 6013 5181 | 本地卡 - Credit |
| 4659 1055 6905 1157 | 外卡 - Debit |
| 4242 4242 4242 4242 | 外卡 - Credit |
| 4870 5270 1770 0692 | Authentication rejected |

详细测试用例参考 [[scn_cko_subscription_test_cards]]。

## 参考资料

- Checkout 官网测试卡：https://www.checkout.com/docs/developer-resources/testing/test-cards
- 开发设计文档：202306-订阅支付
