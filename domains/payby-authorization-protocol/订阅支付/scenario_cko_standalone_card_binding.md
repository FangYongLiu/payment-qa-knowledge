---
id: scn_cko_standalone_card_binding
object_type: Scenario
domain: authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:9770c9b6-cd5c-4f9d-ae94-6d4e4b107220
tags:
- 绑卡
- CKO
- 签约
- token
subdomain: 订阅支付
module: 独立绑卡
sensitivity: normal
name: CKO121独立绑卡场景
aliases: []
related_services: []
related_tables:
- tbl_member_tr_bank_card_token
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
用户在指定业务（支付鉴权配置支持订阅支付的业务）下发起独立绑卡操作，绑卡走 CKO121 签约渠道。

## 前置条件
- 业务方已配置支付鉴权支持订阅支付
- 绑卡渠道路由到 CKO121 签约渠道
- 准备 CKO 测试卡号（参考 [[cko-test-cards]]），例如：
  - 4010 0617 0000 0021（本地卡-Debit）
  - 5385 3083 6013 5181（本地卡-Credit）
  - 4659 1055 6905 1157（外卡-Debit）
  - 4242 4242 4242 4242（外卡-Credit）
  - 4870 5270 1770 0692（Authentication rejected，用于失败用例）

## 操作步骤
1. 用户进入独立绑卡入口，输入卡号等卡信息。
2. 系统将绑卡请求路由至 CKO121 签约渠道。
3. CKO 完成签约处理并返回结果，关键字段 `signTransactionId`。
4. 系统将 `signTransactionId` 加密后作为 token 落库到 `member.tr_bank_card_token`。

## DB 校验点
- 校验 `member.tr_bank_card_token`（[[tbl_member_tr_bank_card_token]]）：
  - 绑卡成功后存在该用户/该卡对应的有效记录
  - token 字段值为 CKO 返回的 `signTransactionId` 加密后的值
- 该表中是否存在有效数据将作为后续支付时该卡是否已签约的判断依据

## 预期结果
- 使用正常测试卡：CKO121 绑卡成功，`member.tr_bank_card_token` 落库一条有效 token 记录。
- 使用 4870 5270 1770 0692（Authentication rejected）：绑卡失败，不在 `member.tr_bank_card_token` 落库有效记录。
- 绑卡成功后，该卡在后续支付过程中可被识别为已签约卡，可走对应 CKO 签约渠道（如 CKO111）替代 moto 渠道场景。
