---
title: MPGS渠道支付测试用例集
domain: acquire-transaction
kind: wiki_page
slug: cgs-apitest-mpgs-channel-cases
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags: []
---

# MPGS渠道支付测试用例集

本页汇总 MPGS 渠道在 cgs-apitest payment 模块下的全部受理用例，覆盖 MPGS101~112 的 3DS2/MOTO 卡支付、MPGS131 设备支付（ApplePay/GooglePay/SamsungPay），以及按卡组织分流到 MPGS101/102/202/204 的拆单路由、MPGS101 退款与 AD 两阶段 Void 等场景。所有用例均通过 SGS `acquire2_placeOrder` 下单，再轮询 `acquire2_getOrder` 直至 `PAID_SUCCESS`/`SETTLED`，并核验 acquireii/tradeii/cmf 多库落库一致性。相关上下文参见 [[cgs-apitest-payment-overview]]。

## 适用场景与渠道分组

- **DirectPay + 3DS2**：本地/国际 MasterCard 与 Visa（MPGS101/102/103/104）。详见 [[scn_mpgs_directpay_3ds2]]。
- **MOTO 免 3DS**：带 CVV (MPGS105/106/107/108) 与不带 CVV (MPGS109/110/111/112)。详见 [[scn_mpgs_moto_payment]]。
- **设备支付**：MPGS131 路由 ApplePay / GooglePay / SamsungPay，`INST_CODE` 分别为 `APPLEPAY` / `GOOGLEPAY` / `SAMSUNGPAY`。详见 [[scn_mpgs_device_pay]]。
- **卡组织拆分路由**：PAYBY MC → MPGS101/102；NI VISA (Lottery 商户) → MPGS202/MPGS204。详见 [[scn_mpgs_cardorg_split]]。
- **退款与 AD Void**：MPGS101 全额/部分退款，PAYPAGE + cardToken AD 两阶段后 Void。详见 [[scn_mpgs_refund_void]]。

## 3DS2 直连支付用例（MPGS101~104）

| 用例 | 方法 | 卡组织 / 类型 |
|---|---|---|
| TC001 | `test_mpgs101_3ds2_success` | Local MasterCard，无 CVV + 3DS2 |
| TC002 | `test_mpgs102_3ds2_success` | International MasterCard，无 CVV + 3DS2 |
| TC003 | `test_mpgs103_3ds2_success` | Local Visa，无 CVV + 3DS2 |
| TC004 | `test_mpgs104_3ds2_success` | International Visa，无 CVV + 3DS2 |

特征：
- `paySceneCode='DIRECTPAY'`，下单同步响应必须 `status=CREATED`。
- 响应需包含 `body.interActionParams.threeDSecureDom`；用正则 `/3ds2/page/([A-Za-z0-9]+)` 提取 `threeDs_id`，否则抛 `3Ds not match`。
- 调用 `MPGS3DS2Client(env).complete_3ds2_authentication(threeDs_id)` 完成持卡人认证。

## MOTO 免 3DS 用例（MPGS105~112）

| 用例 | 方法 | 卡组织 / 类型 |
|---|---|---|
| TC005 | `test_mpgs105_cvv_moto_success` | Local MasterCard 带 CVV |
| TC006 | `test_mpgs106_cvv_moto_success` | International MasterCard 带 CVV |
| TC007 | `test_mpgs107_cvv_moto_success` | Local Visa 带 CVV（末尾 sleep 60s）|
| TC008 | `test_mpgs108_cvv_moto_success` | International Visa 带 CVV |
| TC009 | `test_mpgs109_NoCvv_moto_success` | Local MasterCard 无 CVV |
| TC010 | `test_mpgs110_NoCvv_moto_success` | International MasterCard 无 CVV |
| TC011 | `test_mpgs111_NoCvv_moto_success` | Local Visa 无 CVV |
| TC012 | `test_mpgs112_NoCvv_moto_success` | International Visa 无 CVV（末尾 sleep 60s）|

反向断言：MOTO 用例响应 **不应** 包含 `threeDSecureDom`。

## MPGS131 设备支付用例

| 用例 | 方法 | 设备类型 | INST_CODE |
|---|---|---|---|
| TC013 | `test_mpgs131_ApplePay_success` | ApplePay | APPLEPAY |
| TC014 | `test_mpgs131_GooglePay_success` | GooglePay | GOOGLEPAY |
| TC015 | `test_mpgs131_SamsungPay_success` | SamsungPay | SAMSUNGPAY |
| TC016 | `test_mpgs131_ApplePay_success_riskReject_autoReveral` | ApplePay 风控拒绝 + 自动 Reversal | — （**skip，BUG-8393**）|

下单参数要点：
- `paySceneCode='DIRECTPAY'`，`type` + `devicePayType` 指定通道。
- 卡数据使用 `cardNum / cardExpYear / cardExpMonth`，并传入设备令牌密文 `payCrypt`，由商户公钥 `public_key` 加密。

## 卡组织拆分路由用例

| 用例 | 方法 | 路由目标 | 备注 |
|---|---|---|---|
| TC017 | `test_mpgs_cardOrgSplit_To_mpgs101_PAYBY_MC` | MPGS101 | PAYBY MC + 3DS2 |
| TC018 | `test_mpgs_cardOrgSplit_To_mpgs102_PAYBY_MC` | MPGS102 | PAYBY MC + 3DS2 |
| TC019 | `test_mpgs_cardOrgSplit_To_mpgs202_NI_VISA` | MPGS202 | Lottery 商户 VISA，CAPTURED |
| TC020 | `test_mpgs_cardOrgSplit_To_mpgs204_NI_VISA` | MPGS204 | Lottery 商户 VISA，CAPTURED |

- TC017/TC018 走 3DS2，需提取 `threeDs_id` 并完成挑战。
- TC019/TC020 商户须配置卡组织分流策略到 MPGS202/MPGS204，下单走 DIRECTPAY VISA。

## MPGS101 退款与 AD Void 用例

| 用例 | 方法 | 场景 |
|---|---|---|
| TC021 | `test_mpgs101_transaction_refund_fullAmount` | 支付后全额退款，余额回滚到支付前 |
| TC022 | `test_mpgs101_transaction_refund_PartialAmount` | 按原单金额一半发起部分退款，`inst_order_result` 标记为 `PARTIALLY_REFUNDED` |
| TC023 | `test_mpgs101_requestApiType_AD_then_void` | PAYPAGE + cardToken 走 AD（Authorize+Capture 两阶段）3DS2 流程后发起 Cancel/Void |

校验维度：tradeii 退
