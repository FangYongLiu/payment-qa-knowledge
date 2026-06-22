---
id: scn_mpgs_device_pay
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
- DevicePay
- ApplePay
- GooglePay
- SamsungPay
- DirectPay
subdomain: acquire
module: payment
sensitivity: normal
name: MPGS131 设备支付测试场景
aliases: []
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acs_db
related_scenarios:
- scn_mpgs_directpay_3ds2
- scn_mpgs_moto_payment
- scn_mpgs_cardorg_split
- scn_mpgs_refund_void
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- SGS `acquire2_placeOrder` 接口，`paySceneCode=DIRECTPAY`，并附带设备支付字段：`type`、`devicePayType ∈ {APPLEPAY, GOOGLEPAY, SAMSUNGPAY}`、`cardNum`、`holderName`、`cardExpYear`、`cardExpMonth`、`payCrypt`（设备令牌密文）、`public_key`（RSA 加密用商户公钥）。
- 测试方法：
  - TC013 `test_mpgs131_ApplePay_success`
  - TC014 `test_mpgs131_GooglePay_success`
  - TC015 `test_mpgs131_SamsungPay_success`
  - TC016 `test_mpgs131_ApplePay_success_riskReject_autoReveral`（**skip**, BUG-8393）

## 前置条件
- Fixtures：`self.sgs`、`self.mpgs_3ds`、`self.db_instance_factory('select')`、`self.test_data[<method_name>]`、`self.wait_for_order_success`。
- 商户在 `acs.t_key_config` 配置 PRIVATE 证书（`CERT_TYPE='PRIVATE'`, `enable_flag='Y'`），用于设备密文/卡数据 RSA 加密，按 `PARTNER_ID` 查询 `RELATE_CERT`。
- 商户需开通：Auto Debit、Direct Pay Domestic Card、Direct Pay INTL Card 等产品。
- 测试数据包含 partnerId、amount 以及设备支付密文 (`payCrypt`) 等。
- 全部用例使用 `@pytest.mark.uat`。

## 操作步骤
1. 从 `self.test_data` 取该用例参数（partnerId、amount、devicePayType、cardNum、holderName、cardExpYear、cardExpMonth、payCrypt 等）。
2. 调用 `sgs.acquire2_placeOrder(partnerId, amount, paySceneCode='DIRECTPAY', type=..., devicePayType=APPLEPAY|GOOGLEPAY|SAMSUNGPAY, cardNum, holderName, cardExpYear, cardExpMonth, payCrypt, public_key)`。
3. 校验同步响应：`status == "CREATED"`，记录 `body.acquireOrder.orderNo` 与 `body.acquireOrder.merchantOrderNo`。
4. 设备支付免 3DS，**不进入** `mpgs_3ds.complete_3ds2_authentication`。
5. 调用 `self.wait_for_order_success(partnerId, orderNo, mode='SGS')` 轮询订单至终态。
6. TC016：成功路径完成后由风控拒绝触发自动 Reversal，验证订单链路最终为失败/冲正态。

## DB 校验点
- 跨 `acquireii / tradeii / cmf` 库一致性核验：
  - `acquireii.t_acquire_order`：订单成功落库，`FUND_CHANNEL_CODE=MPGS131`。
  - `tradeii.t_trade_order`：`trade_status='SS'`。
  - `cmf.tt_cmf_order`：主单 `STATUS='S'`。
  - `cmf.tt_inst_order` / `cmf.tt_inst_order_result`：`INST_CODE` 分别为 `APPLEPAY` / `GOOGLEPAY` / `SAMSUNGPAY`，结果成功。
- TC016 自动冲正路径下，订单链路落为失败/冲正终态（具体状态依 BUG-8393 修复后口径）。

## 预期结果
- TC013/TC014/TC015：设备支付下单同步返回 `status=CREATED`，免 3DS（响应不应包含 `threeDSecureDom`）；订单终态为 `PAID_SUCCESS` 或 `SETTLED`；资金渠道路由到 MPGS131，`INST_CODE` 与所选 `devicePayType` 对应。
- TC016（skip）：ApplePay 支付成功后被风控拒绝，触发自动 Reversal，订单最终为失败 / 已冲正状态。
