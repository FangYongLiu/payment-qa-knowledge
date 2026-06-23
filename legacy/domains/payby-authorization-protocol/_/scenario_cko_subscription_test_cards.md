---
id: scn_cko_subscription_test_cards
object_type: Scenario
domain: authorization-protocol
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/1082523699
tags:
- CKO
- 订阅支付
- 测试卡
subdomain: null
module: null
sensitivity: normal
name: CKO订阅支付测试卡用例
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
在 CKO Channel 订阅支付（[[cko-channel-subscription-payment]]）相关流程中，需要使用测试卡号进行绑卡、收银台卡支付以及鉴权拒绝场景验证时使用。

## 前置条件
- 业务方已配置支持订阅支付的支付鉴权
- 已接入 CKO 签约渠道（如 CKO121 用于独立绑卡，CKO111 用于 moto 渠道）
- 参考 Checkout 官网测试卡信息：https://www.checkout.com/docs/developer-resources/testing/test-cards

## 操作步骤
使用以下测试卡号进行对应场景测试：

| Card No | Discript |
|---|---|
| 4010 0617 0000 0021 | 本地卡-Debit |
| 5385 3083 6013 5181 | 本地卡-Credit |
| 4659 1055 6905 1157 | 外卡-Debit |
| 4242 4242 4242 4242 | 外卡-Credit |
| 4870 5270 1770 0692 | Authentication rejected |

## DB 校验点
- 独立绑卡（CKO121）成功后，校验 `member.tr_bank_card_token` 表中是否落库（CKO 返回字段 `signTransactionId` 加密后作为 token 落地）
- 后续支付过程中以该表是否存在有效数据作为该卡是否已签约的判断依据

## 预期结果
- 本地卡（Debit/Credit）和外卡（Debit/Credit）：可正常完成绑卡及收银台卡支付流程
- Authentication rejected 卡号 `4870 5270 1770 0692`：鉴权被拒绝，用于验证鉴权失败场景
- 独立绑卡成功后 `member.tr_bank_card_token` 应有对应签约 token 落地
