---
id: scn_mpgs_directpay_3ds2
object_type: Scenario
domain: acquire-transaction
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags:
- mpgs
- directpay
- 3ds2
- fundin
- mastercard
- visa
subdomain: mpgs-channel
module: payment
sensitivity: normal
name: MPGS DirectPay 3DS2 支付测试场景
aliases:
- MPGS101-104 DirectPay 3DS2
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_card_info
- tbl_cmf_tt_inst_order
- tbl_cmf_tt_inst_order_result
related_scenarios:
- scn_mpgs_moto_payment
- scn_mpgs_device_pay
- scn_mpgs_cardorg_split
- scn_mpgs_refund_void
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
通过 SGS `acquire2_placeOrder` 接口以 `paySceneCode='DIRECTPAY'` 提交直连卡支付下单，传入完整卡四要素（cardNo、holderName、expYear、expMonth），但**不带 CVV**，触发 MPGS 渠道的 3DS2 验证流程。

测试方法（test_mpgs_channel_xxx.py）：
- `test_mpgs101_3ds2_success` (TC001) — MPGS101 Local MasterCard 无 CVV + 3DS2
- `test_mpgs102_3ds2_success` (TC002) — MPGS102 International MasterCard 无 CVV + 3DS2
- `test_mpgs103_3ds2_success` (TC003) — MPGS103 Local Visa 无 CVV + 3DS2
- `test_mpgs104_3ds2_success` (TC004) — MPGS104 International Visa 无 CVV + 3DS2

均带 `@pytest.mark.uat` 标记，定位 UAT 环境运行。

## 前置条件
- Fixtures（`setup` autouse）：注入 `CGSapi`、`SGS`、`MPGS3DS2Client(env)`、`RSA_encrypt`、`Module`、`db_instance_factory`、`get_testdata`、`get_urls`（cgs_url、sgs_url）。
- 商户密钥：`acs.t_key_config` 中按 `PARTNER_ID` 查询 `CERT_TYPE='PRIVATE'`、`enable_flag='Y'` 的 RELATE_CERT，用作 `public_key` 对卡敏感数据进行 RSA 加密。
- 商户已开通 Direct Pay Domestic Card / Direct Pay INTL Card 产品。
- 测试数据按方法名取 `(partnerId, amount, cardNo, holderName, cvv, expYear, expMonth)`，本组用例下单时不传 cvv。

## 操作步骤
1. **下单**：调用 `sgs.acquire2_placeOrder(partnerId, amount, paySceneCode='DIRECTPAY', cardNo, holderName, expYear, expMonth, public_key=...)`。
   - 期望同步响应 `body.acquireOrder.status == "CREATED"`。
   - 取 `body.acquireOrder.orderNo`、`body.acquireOrder.merchantOrderNo`。
   - 必须返回 `body.interActionParams.threeDSecureDom`，含 `/3ds2/page/<threeDsId>` 链接。
2. **解析 3DS2 ID**：用正则 `/3ds2/page/([A-Za-z0-9]+)` 从 `threeDSecureDom` 中提取 `threeDs_id`；匹配失败抛 "3Ds not match"。
3. **完成 3DS2 认证**：调用 `MPGS3DS2Client(env).complete_3ds2_authentication(threeDs_id)` 模拟持卡人在 MPGS 3DS2 页面完成认证。
4. **轮询订单终态**：`wait_for_order_success(partnerId, orderNo, mode='SGS', timeout=300, interval=2)`，通过 `sgs.acquire2_getOrder(partnerId, orderNo)` 轮询，直至状态为 `PAID_SUCCESS` 或 `SETTLED`；超时抛 AssertionError 并附最终状态。

## DB 校验点
通过 `db_instance_factory('select')` 跨库核验全链路落库一致性：
- `acquireii.t_acquire_order`：订单存在，状态为成功终态。
- `tradeii.t_trade_order`：`trade_status='SS'`。
- `cmf.tt_cmf_order`：主单 `STATUS='S'`。
- `cmf.tt_inst_order`：指令落库，`FUND_CHANNEL_CODE` 与用例对应（MPGS101 / MPGS102 / MPGS103 / MPGS104）。
- `cmf.tt_inst_order_result`：指令结果成功。

## 预期结果
- `placeOrder` 同步返回 `status=CREATED` 且响应中包含 `threeDSecureDom`（与 MOTO 场景反向：MOTO 不应包含）。
- 3DS2 认证完成后订单进入 `PAID_SUCCESS` / `SETTLED` 终态。
- `FUND_CHANNEL_CODE` 按卡 BIN/卡组织正确路由：
  - MPGS101 = Local MasterCard
  - MPGS102 = International MasterCard
  - MPGS103 = Local Visa
  - MPGS104 = International Visa
- acquireii → tradeii → cmf 三层订单/指令/结果数据一致，资金渠道码与用例预期匹配。
