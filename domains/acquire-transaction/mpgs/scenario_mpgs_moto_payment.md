---
id: scn_mpgs_moto_payment
object_type: Scenario
domain: acquire-transaction
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags:
- mpgs
- moto
- directpay
- acquire
- fundin
subdomain: mpgs
module: payment
sensitivity: normal
name: MPGS MOTO 免3DS支付测试场景
aliases:
- MPGS105-112 MOTO
- MOTO免3DS
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_card_info
- tbl_cmf_tt_inst_order
- tbl_cmf_tt_inst_order_result
- tbl_acs_db
related_scenarios:
- scn_mpgs_directpay_3ds2
- scn_mpgs_device_pay
- scn_mpgs_cardorg_split
- scn_mpgs_refund_void
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- 测试文件：cgs-apitest `testcases/payment` 下 MPGS 渠道支付用例集（`scn_mpgs_channel_cases`）。
- 入口接口：[[api_acquire_place_order]] SGS `/acquire2/placeOrder`，`paySceneCode='DIRECTPAY'`。
- 用例编号与方法：
  - TC005 `test_mpgs105_cvv_moto_success` — MPGS105 Local MasterCard 带 CVV 免 3DS MOTO 成功
  - TC006 `test_mpgs106_cvv_moto_success` — MPGS106 International MasterCard 带 CVV 免 3DS MOTO 成功
  - TC007 `test_mpgs107_cvv_moto_success` — MPGS107 Local Visa 带 CVV 免 3DS MOTO 成功（末尾 sleep 60s）
  - TC008 `test_mpgs108_cvv_moto_success` — MPGS108 International Visa 带 CVV 免 3DS MOTO 成功
  - TC009 `test_mpgs109_NoCvv_moto_success` — MPGS109 Local MasterCard 无 CVV 免 3DS MOTO 成功
  - TC010 `test_mpgs110_NoCvv_moto_success` — MPGS110 International MasterCard 无 CVV 免 3DS MOTO 成功
  - TC011 `test_mpgs111_NoCvv_moto_success` — MPGS111 Local Visa 无 CVV 免 3DS MOTO 成功
  - TC012 `test_mpgs112_NoCvv_moto_success` — MPGS112 International Visa 无 CVV 免 3DS MOTO 成功（末尾 sleep 60s）
- 标记：`@pytest.mark.uat`。

## 前置条件
- `setup`（autouse）注入：`CGSapi`、`SGS`、`MPGS3DS2Client(env)`、`RSA_encrypt`、`Module`、`db_instance_factory`、`get_testdata`、`get_urls`（cgs_url, sgs_url）。
- 商户密钥：从 `acs.t_key_config` 按 `PARTNER_ID` 查询 `CERT_TYPE='PRIVATE'`、`enable_flag='Y'` 的 `RELATE_CERT`，用于卡数据 RSA 加密（`public_key` 入参）。
- 商户需开通产品：Direct Pay Domestic Card、Direct Pay INTL Card（按卡类型/本地国际匹配）。
- 测试数据按方法名取参数化元组：
  - 带 CVV 用例（TC005-TC008）：`(partnerId, amount, cardNo, holderName, cvv, expYear, expMonth)`
  - 不带 CVV 用例（TC009-TC012）：`(partnerId, amount, cardNo, holderName, expYear, expMonth)`，无 `cvv` 字段。

## 操作步骤
1. 用商户 PRIVATE 证书（`public_key`）对卡敏感数据进行 RSA 加密。
2. 调用 `self.sgs.acquire2_placeOrder(partnerId, amount, paySceneCode='DIRECTPAY', cardNo, [cvv,] holderName, expYear, expMonth, public_key=...)`：
   - 带 CVV 路径（TC005-TC008）：传入 `cvv`，但走 MOTO 通道，**响应不应包含 `threeDSecureDom`**。
   - 不带 CVV 路径（TC009-TC012）：不传 `cvv`，同样 **响应不应包含 `threeDSecureDom`**。
3. 断言下单同步响应 `body.acquireOrder.status == "CREATED"`，取出 `orderNo`、`merchantOrderNo`。
4. 反向断言：响应中不存在 `threeDSecureDom`（不进入 3DS2 流程），无需调用 `MPGS3DS2Client.complete_3ds2_authentication`。
5. 调用 `self.wait_for_order_success(partnerId, orderNo, mode='SGS', timeout=300, interval=2)` 轮询，直到 `acquireOrder.status` 为 `PAID_SUCCESS` 或 `SETTLED`；超时抛 `AssertionError` 并附最终状态与响应。
6. TC007/TC012 末尾 `sleep 60s` 等待后续异步落库稳定。

## DB 校验点
按 `FUND_CHANNEL_CODE = MPGS105 / MPGS106 / MPGS107 / MPGS108 / MPGS109 / MPGS110 / MPGS111 / MPGS112` 分别校验路由结果，跨库一致性核验：
- `acquireii.t_acquire_order`：主单存在，订单状态推进至支付成功终态。
- `tradeii.t_trade_order`：`trade_status='SS'`。
- `cmf.tt_cmf_order`：主单 `STATUS='S'`。
- `cmf.tt_inst_order` / `cmf.tt_inst_order_result`：按用例预期的 `FUND_CHANNEL_CODE` 落库，渠道结果为成功。
- `acs.t_key_config`：仅作前置读取以获取 PRIVATE 证书。

## 预期结果
- 下单同步响应 `status == "CREATED"`，并 **不返回 `threeDSecureDom`**（MOTO 免 3DS）。
- 订单按卡类型（Local/International）与卡组织（MasterCard/Visa）以及是否带 CVV，准确路由到对应 MPGS 子渠道：MPGS105–MPGS112。
- 终态：SGS 端 `acquireOrder.status ∈ {PAID_SUCCESS, SETTLED}`；trade 表 `trade_status='SS'`；cmf 主单 `STATUS='S'`。
- 全链路 acquireii → tradeii → cmf 数据落库一致，`FUND_CHANNEL_CODE` 与用例预期 MPGS 子渠道一致。
