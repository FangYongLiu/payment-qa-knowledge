---
id: scn_online_business_merchant_payout
object_type: Scenario
name: 商户出款 / 转账 (Transfer / Payout)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-03'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_transfer_{order,to_bank,to_card}_fangyong.py (UAT 实跑 2026-07-03)
tags: [online-business, 支付, cgs-apitest, 实测]
related_services: [svc_fundout, svc_merchant_fundout, svc_remittance, svc_tradeii, svc_payment, svc_cards]
related_tables: []
related_logs: []
---

# 商户出款 / 转账 (Transfer / Payout)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 出款/转账:转账下单(到手机号/TOTOK UID/公司MID/个人MID)、转账到银行(本币AED/USD、SWIFT USD)、转账到卡(个人/对公、卡资格校验、卡token)。经 fundout/merchant-fundout + remittance 通道。

## 关联关系
- **涉及服务**:[[svc_fundout]]、[[svc_merchant_fundout]]、[[svc_remittance]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cards]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:由覆盖本场景的 AutomationAsset 在其 `related_scenarios` 中声明。
- **读写的表**:待补

## 实测(UAT 2026-07-03,test_transfer_*)—— 11 passed / 4 failed(失败均测试数据 KeyError,非缺陷)
出款按目标分四类产品(response `product`),接口前缀 `/sgs/api/transfer/*`:
| 产品 | 接口 | 目标 | 实测 |
| --- | --- | --- | --- |
| **Transfer**(转钱包) | `placeTransferOrder` | 手机号 / MID→个人 / MID→公司 | 订单 `status=SUCCESS` |
| **Transfer To Bank**(本地) | `placeTransferToBankOrder` | IBAN,`networkCode=LOCAL`,AED | SUCCESS |
| **Transfer To Internationale Bank Via SWIFT** | `placeTransferToBankOrder` | accountNo,`networkCode=SWIFT`,USD | SUCCESS |
| **Transfer Bank Card** | `placeTransferToCard` / `placeTransferToBankCard` | 卡号 / 卡token,个人/对公 | SUCCESS |

- **失败项均为 cgs 测试数据缺失**(`KeyError: test_placeTransferOrder_TOTOKUID`、`..._UseCardToken`),非产品问题。
- **VAM Xtran**(`/vam/applyVamXtran`,虚拟账户)本轮通过,但 **VAM 属 deposit-vam 域**,不在收单域展开。
- 转账/出款渠道 Mock 触发规则(有效期/金额→错误码)见 [[reference_fundout_channel_mock_rules]];请求样例见 [[reference_acquire_payscene_request_examples]] 转账小节。

## 校验点(QA)
- placeTransferOrder 各收款方类型;到银行 本币(LOCAL/AED)/SWIFT(USD)币种与通道。
- 到卡资格校验(Standard/FastFunds);卡token 复用;CORPORATE sender 渠道侧支持度(payee CORPORATE 不支持,见样例手册)。
- 出款单状态与回调;卡在 process 的人工处理见 [[ts_fundout_stuck_in_process]]。

## 来源与置信
- **UAT 实跑 2026-07-03**(transfer order/bank/card 套件,11 passed):产品/接口/状态为实测;失败为测试数据缺失。
