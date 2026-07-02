---
id: scn_cko_card_binding_subscription
object_type: Scenario
name: CKO 订阅支付绑卡与签约（CKO121/CKO111）
aliases:
- CKO独立绑卡
- CKO订阅支付
- CKO测试卡
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/1082523699 + wiki:9770c9b6-cd5c-4f9d-ae94-6d4e4b107220
tags:
- CKO
- 绑卡
- 订阅支付
- 签约
- 测试卡
related_services:
- svc_cmf
- svc_member
related_tables:
- tbl_member_tr_bank_card_token
related_logs: []
---

# CKO 订阅支付绑卡与签约（CKO121/CKO111）

## 触发 / 入口

针对「支付鉴权配置支持订阅支付」的业务：用户使用**已签约银行卡**走 moto 渠道场景时，可走 CKO 对应签约渠道。等价于在原渠道基础上多一个 moto 渠道。两类操作：
- **独立绑卡**：走 CKO121 签约渠道。
- **收银台卡支付**：用已签约卡走 CKO 对应签约渠道（如 CKO111）替代 moto 渠道。

端到端时序见 [[flow_cko_subscription_payment]]。

## 关联关系

- **涉及服务**：[[svc_cmf]]（卡信息 / token 落库）、[[svc_member]]（会员卡）（= `related_services`）
- **校验的表**：[[tbl_member_tr_bank_card_token]]（= `related_tables`）
- **相关流程**：[[flow_cko_subscription_payment]]

## 前置条件

- 业务方已配置支付鉴权支持订阅支付。
- 已接入 CKO 签约渠道（CKO121 用于独立绑卡，CKO111 用于 moto 渠道）。
- 准备 CKO 测试卡号（参考 Checkout 官网 https://www.checkout.com/docs/developer-resources/testing/test-cards）：

| Card No | 说明 |
|---|---|
| 4010 0617 0000 0021 | 本地卡 - Debit |
| 5385 3083 6013 5181 | 本地卡 - Credit |
| 4659 1055 6905 1157 | 外卡 - Debit |
| 4242 4242 4242 4242 | 外卡 - Credit |
| 4870 5270 1770 0692 | Authentication rejected（鉴权拒绝，用于失败用例） |

## 操作步骤

1. 用户进入独立绑卡入口，输入卡号等卡信息。
2. 系统将绑卡请求路由至 CKO121 签约渠道。
3. CKO 完成签约处理并返回结果，关键字段 `signTransactionId`。
4. 系统将 `signTransactionId` 加密后作为 token 落库到 `member.tr_bank_card_token`。
5. 后续支付时，以该表是否存在有效数据作为该卡「是否已签约」的判断依据。

## DB 校验点

- [[tbl_member_tr_bank_card_token]]：
  - 绑卡成功后存在该用户/该卡对应的有效 token 记录，token 值为 CKO 返回 `signTransactionId` 加密后的值。
  - 该表存在有效数据 = 该卡已签约。

## 预期结果

- 正常测试卡：CKO121 绑卡成功，`member.tr_bank_card_token` 落一条有效 token；该卡后续支付可被识别为已签约卡，可走 CKO 签约渠道（如 CKO111）替代 moto。
- `4870 5270 1770 0692`（Authentication rejected）：绑卡失败，不在表中落有效记录，用于验证鉴权失败场景。
