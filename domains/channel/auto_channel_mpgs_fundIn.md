---
id: auto_channel_mpgs_fundIn
object_type: AutomationAsset
name: MPGS 充值入金自动化
aliases: [test_mpgs_fundIn_fangyong]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/fundChannel/test_mpgs_fundIn_fangyong.py
tags: [channel, 自动化, cgs-apitest]
related_scenarios: [scn_channel_fund_in]
related_services: [svc_qpay_cko, svc_qpay_mpgs, svc_acquireii, svc_tradeii, svc_payment]
---

# MPGS 充值入金自动化

> 来源 cgs-apitest `fundChannel/test_mpgs_fundIn_fangyong.py`(23 TC)。覆盖 [[scn_channel_fund_in]]。

## 用途
对「渠道充值入金 (Fund-In)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_mpgs101_3ds2_success` | TC001:MPGS101-Local-MasterCard-NoCVV-3Ds |
| 2 | `test_mpgs102_3ds2_success` | TC002:MPGS102-International-MasterCard-NoCVV-3Ds |
| 3 | `test_mpgs103_3ds2_success` | TC003:MPGS103-Local-VisaCard-NoCVV-3Ds |
| 4 | `test_mpgs104_3ds2_success` | TC004:MPGS104-International-VisaCard-NoCVV-3Ds |
| 5 | `test_mpgs105_cvv_moto_success` | TC005:MPGS105-Local-MasterCard-CVV-No3Ds-MOTO |
| 6 | `test_mpgs106_cvv_moto_success` | TC006:MPGS106-International-MasterCard-CVV-No3Ds-MOTO |
| 7 | `test_mpgs107_cvv_moto_success` | TC007:MPGS107-Local-VisaCard-CVV-No3Ds-MOTO |
| 8 | `test_mpgs108_cvv_moto_success` | TC008:MPGS108-International-VisaCard-CVV-No3Ds-MOTO |
| 9 | `test_mpgs109_NoCvv_moto_success` | TC009:MPGS109-Local-MasterCard-NoCVV-No3Ds-MOTO |
| 10 | `test_mpgs110_NoCvv_moto_success` | TC010:MPGS110-International-MasterCard-NoCVV-No3Ds-MOTO |
| 11 | `test_mpgs111_NoCvv_moto_success` | TC011:MPGS111-Local-VisaCard-NoCVV-No3Ds-MOTO |
| 12 | `test_mpgs112_NoCvv_moto_success` | TC012:MPGS112-International-VisaCard-NoCVV-No3Ds-MOTO |
| 13 | `test_mpgs131_ApplePay_success` | TC013:MPGS131-ApplePay-Channel |
| 14 | `test_mpgs131_GooglePay_success` | TC014:MPGS131-GooglePay-Channel |
| 15 | `test_mpgs131_SamsungPay_success` | TC015:MPGS131-SamsungPay-Channel |
| 16 | `test_mpgs131_ApplePay_success_riskReject_autoReveral` | TC016:MPGS131-ApplePay-Success-RiskReject-AutoReversal |
| 17 | `test_mpgs_cardOrgSplit_To_mpgs101_PAYBY_MC` | TC017: cardOrgSplit_To_mpgs101_PAYBY_MC(For Lottery) |
| 18 | `test_mpgs_cardOrgSplit_To_mpgs102_PAYBY_MC` | TC018:cardOrgSplit_To_mpgs102_PAYBY_MC(For Lottery) |
| 19 | `test_mpgs_cardOrgSplit_To_mpgs202_NI_VISA` | TC019:cardOrgSplit_To_mpgs202_NI_VISA(For Lottery) |
| 20 | `test_mpgs_cardOrgSplit_To_mpgs204_NI_VISA` | TC020:cardOrgSplit_To_mpgs204_NI_VISA(For Lottery) |
| 21 | `test_mpgs101_transaction_refund_fullAmount` | TC021:MPGS101-ChannelTransaction-Refund-FullAmount |
| 22 | `test_mpgs101_transaction_refund_PartialAmount` | TC022:MPGS101-ChannelTransaction-Refund-PartialAmount |
| 23 | `test_mpgs101_requestApiType_AD_then_void` | TC023:MPGS101-Cmf-RequestApiType-AD-then-Void-FullAmount |

## 关联关系
- **覆盖的场景**:[[scn_channel_fund_in]]
- **针对/跑在的服务**:[[svc_qpay_cko]]、[[svc_qpay_mpgs]]、[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]

## 使用方式
- 入口:`pytest testcases/payment/fundChannel/test_mpgs_fundIn_fangyong.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `fundChannel/test_mpgs_fundIn_fangyong.py`;TC 来自源码。
