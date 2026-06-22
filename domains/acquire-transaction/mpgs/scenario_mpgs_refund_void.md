---
id: scn_mpgs_refund_void
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
- refund
- void
- authorize-capture
- paypage
- 3ds2
subdomain: mpgs
module: payment
sensitivity: normal
name: MPGS101 退款与AD两阶段Void测试场景
aliases: []
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_void_order
- tbl_cmf_tt_inst_order
- tbl_cmf_tt_inst_order_result
- tbl_acs_db
related_scenarios:
- scn_mpgs_directpay_3ds2
- scn_mpgs_moto_payment
- scn_mpgs_cardorg_split
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
SGS `acquire2/placeOrder` 下单，`paySceneCode` 为 `DIRECTPAY`（TC021/TC022）或 `PAYPAGE`（TC023），路由进入 MPGS101 子渠道；支付成功后调用退款下单接口发起 Refund 或 Cancel(Void)。

## 前置条件
- `self.test_data` 按方法名提供参数：partnerId、amount、cardNo、holderName、cvv、expYear、expMonth、cardToken（TC023 PAYPAGE）。
- `self.sgs` / `self.cgs` / `self.mpgs_3ds` / `self.db_instance_factory('select' | 'tradeii')`、`self.wait_for_order_success` 已注入。
- 商户在 `acs.t_key_config` 配置 `CERT_TYPE='PRIVATE'`、`enable_flag='Y'` 的 RELATE_CERT 用于敏感数据 RSA 加签/加密。
- 商户开通 Direct Pay / PAYPAGE 等支付产品，并在 dpm 开通 AED 外部账户。
- MPGS101 子渠道（Local MasterCard）可用。

## 操作步骤
**TC021 — MPGS101 全额退款**
1. 通过 `sgs.acquire2_placeOrder(partnerId, amount, paySceneCode='DIRECTPAY', cardNo, cvv, holderName, expYear, expMonth, public_key=...)` 下单，期望响应 `status=CREATED`。
2. 从返回 `body.interActionParams.threeDSecureDom` 中正则提取 `/3ds2/page/<threeDs_id>`，调用 `mpgs_3ds.complete_3ds2_authentication(threeDs_id)` 完成 3DS2 认证。
3. `wait_for_order_success(partnerId, orderNo, mode='SGS')` 轮询到支付终态 `PAID_SUCCESS` / `SETTLED`。
4. 调用退款下单接口（refund_place_order），按原订单全额退款。
5. 轮询退款订单直至成功。

**TC022 — MPGS101 部分退款**
1. 步骤 1–3 同 TC021。
2. 发起退款金额 = 原单金额的 1/2。
3. 轮询退款订单成功。

**TC023 — MPGS101 PAYPAGE + cardToken AD → Void**
1. `sgs.acquire2_placeOrder(...)` 使用 `paySceneCode='PAYPAGE'` 并携带 cardToken，触发渠道 AD 模式（Authorize + Capture 两阶段）。
2. 走 3DS2 认证流程（同上）。
3. 等待 Authorize+Capture 推进完成、订单达到成功终态。
4. 发起退款（Cancel/Void）下单，等待退款成功。

## DB 校验点
- `acquireii.t_acquire_order`：主订单 `FUND_CHANNEL_CODE=MPGS101`，订单达到支付终态。
- `acquireii.t_refund_order`（TC021/TC022/TC023）：退款订单生成且状态成功；TC022 退款金额为原单金额一半。
- `acquireii.t_void_order`（TC023）：AD 模式下 Void/Cancel 记录落库。
- `cmf.tt_inst_order` / `cmf.tt_inst_order_result`：
  - TC021/TC023：退款后主单及指令结果对应退款/撤销状态。
  - TC022：`tt_inst_order_result` 标记为 `PARTIALLY_REFUNDED`。
- `tradeii` 库交易状态与退款一致。

## 预期结果
- TC021：支付成功后全额退款成功，余额回滚至支付前。
- TC022：部分退款（一半金额）成功，指令结果为 `PARTIALLY_REFUNDED`。
- TC023：PAYPAGE + cardToken 触发 AD（Authorize+Capture）+ 3DS2 成功后，发起 Cancel/Void 退款成功，多表（acquire/refund/void/cmf）数据一致。
