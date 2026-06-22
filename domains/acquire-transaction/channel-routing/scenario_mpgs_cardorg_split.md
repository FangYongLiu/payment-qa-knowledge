---
id: scn_mpgs_cardorg_split
object_type: Scenario
domain: acquire-transaction
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags:
- MPGS
- DirectPay
- 3DS2
- 卡组织路由
- Lottery
subdomain: channel-routing
module: payment
sensitivity: normal
name: MPGS卡组织拆分路由测试场景
aliases: []
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acs_db
related_scenarios:
- scn_mpgs_directpay_3ds2
- scn_mpgs_refund_void
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
来自 `cgs-apitest` 仓库 `testcases/payment` 下的 MPGS 渠道用例，覆盖 Lottery 商户在 DirectPay + 3DS2 流程下，按卡组织（MasterCard / Visa）拆单路由到不同 MPGS 子渠道：

- TC017 `test_mpgs_cardOrgSplit_To_mpgs101_PAYBY_MC`：PAYBY MC 卡组织拆分到 MPGS101。
- TC018 `test_mpgs_cardOrgSplit_To_mpgs102_PAYBY_MC`：PAYBY MC 卡组织拆分到 MPGS102。
- TC019 `test_mpgs_cardOrgSplit_To_mpgs202_NI_VISA`：Lottery VISA 卡 DIRECTPAY 路由到 MPGS202。
- TC020 `test_mpgs_cardOrgSplit_To_mpgs204_NI_VISA`：Lottery VISA 卡 DIRECTPAY 路由到 MPGS204。

## 前置条件
- 商户为 Lottery 业务并配置了卡组织分流策略，可分别路由到 MPGS101 / MPGS102（MC）与 MPGS202 / MPGS204（VISA）。
- 商户已开通：Auto Debit、Direct Pay Domestic Card、Direct Pay INTL Card 等产品。
- `acs.t_key_config` 中按 `partnerId` 配置了 `CERT_TYPE='PRIVATE'`、`enable_flag='Y'` 的 RELATE_CERT，用于卡敏感数据 RSA 加签/加密。
- Fixtures：`self.sgs`、`self.mpgs_3ds`（含 `complete_3ds2_authentication`）、`self.db_instance_factory('select')`、`self.test_data[<method_name>]`、`self.wait_for_order_success`。
- 测试数据按方法名提供 `(partnerId, amount, cardNo, holderName, cvv, expYear, expMonth)`，且必须传入 `cvv` 以触发 3DS2。
- 用例标记 `@pytest.mark.uat`。

## 操作步骤
1. 调用 `sgs.acquire2_placeOrder(partnerId, amount, paySceneCode='DIRECTPAY', cardNo, cvv, holderName, expYear, expMonth, public_key=<商户 PRIVATE 证书>)` 下单。
2. 断言响应 `body.acquireOrder.status == "CREATED"`，提取 `orderNo`、`merchantOrderNo`，以及 `body.interActionParams.threeDSecureDom`。
3. 用正则 `/3ds2/page/([A-Za-z0-9]+)` 从 `threeDSecureDom` 中提取 `threeDs_id`；若未匹配抛 "3Ds not match"。
4. 调用 `mpgs_3ds.complete_3ds2_authentication(threeDs_id)` 完成持卡人 3DS2 认证。
5. 调用 `wait_for_order_success(partnerId, orderNo, mode='SGS')` 轮询订单直至终态。

## DB 校验点
按 `merchantOrderNo` / `orderNo` 关联校验全链路落库：
- `acquireii.t_acquire_order`：订单存在，金额、商户号一致。
- `tradeii.t_trade_order`：`trade_status='SS'`。
- `cmf.tt_cmf_order`：主单 `STATUS='S'`。
- `cmf.tt_inst_order` / `cmf.tt_inst_order_result`：`FUND_CHANNEL_CODE` 按用例分别为 `MPGS101` / `MPGS102` / `MPGS202` / `MPGS204`，证明卡组织拆分路由生效。

## 预期结果
- 下单同步响应 `status == "CREATED"`，并返回 `threeDSecureDom`（3DS2 触发）。
- 3DS2 认证完成后，SGS 端 `acquireOrder.status` 进入终态 `PAID_SUCCESS` 或 `SETTLED`（TC019/TC020 描述为 CAPTURED 成功）。
- 资金渠道码按卡组织正确分流：
  - PAYBY MasterCard → MPGS101（TC017）/ MPGS102（TC018）
  - NI VISA（Lottery）→ MPGS202（TC019）/ MPGS204（TC020）
- acquire → trade → cmf 三层订单全部成功落库且状态一致。
