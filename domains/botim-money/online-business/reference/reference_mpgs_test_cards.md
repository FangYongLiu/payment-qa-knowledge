---
id: reference_mpgs_test_cards
object_type: Reference
name: MPGS 渠道官方测试卡 (Mastercard Gateway Test Cards)
aliases: [MPGS test cards, mastercard gateway test cards, MPGS 测试卡]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
source_type: reference
source_ref: 'https://mtf.gateway.mastercard.com/api/documentation/integrationGuidelines/supportedFeatures/testAndGoLive.html (fetched 2026-07-03)'
tags: [online-business, 收单, MPGS, 测试卡, test-card, card-payment]
related_services: [svc_acquireii, svc_qpay_mpgs]
related_scenarios: [scn_online_business_mpgs_channel, scn_mpgs_onboarding]
---

# MPGS 渠道官方测试卡 (Mastercard Gateway Test Cards)

商户收单卡支付测试用的 **MPGS(Mastercard Payment Gateway Services)官方测试卡**。用于 [[svc_qpay_mpgs]] 渠道、[[svc_acquireii]] 收单核心的卡支付/3DS/退款测试,场景见 [[scn_online_business_mpgs_channel]] / [[scn_mpgs_onboarding]]。

> **仅 MTF 测试环境使用,禁止在生产用这些卡。** 使用测试商户档案(Merchant ID 前缀 `TEST`)。
> 关键机制:**用不同的到期日 / CSC(CVV)/ 账单地址街道名 来触发不同响应**(卡号固定,结果由这些字段决定)。数据源见 frontmatter `source_ref`。

## 标准测试卡(所有支持区域)
| 卡组织 | 卡号 |
| --- | --- |
| Mastercard | `5123450000000008` / `2223000000000007` / `5111111111111118` / `2223000000000023` |
| Visa | `4508750015741019` / `4012000033330026` |
| American Express | `371881634498004` / `371881127160004` / `371881245560002` / `371881911767006` |
| Diners Club | `30123400000000` / `36259600000012` |
| JCB | `3528000000000007` / `3528111100000001` |
| Discover | `6011003179988686` / `6011963280099774` |
| Maestro | `5000000000000000005` / `5666555544443333` |
| UATP(不支持 CSC/CVV、3DS) | `135492354874528` / `135420001569134` |
| UnionPay 3DS enrolled | `6201089999995464` / `6201089999991455` / `6201089999994020` / `6201089999999300` / `6201089999994749` |
| UnionPay 非 3DS | `6214239999999611` / `6214239999999546` |

## UAE 本地卡(Mada / Jaywan —— 与 AstraTech 本地收单相关)
| 类型 | 卡号 |
| --- | --- |
| Mada Mastercard | `5297410588409146` / `5433579999990250` / `5433570000000008` |
| Mada Visa | `4228180191362993` / `4860940000000008` / `4860940000000024` |
| Mada Only | `9682090000000007` / `8736469999990336` / `9682090000000031` |
| Jaywan mono-badge 3DS enrolled | `6690109900000010` / `6690109000011008` / `6690109000011016` / `6690109000011024` / `6690109000011032` |
| Jaywan mono-badge 非 3DS | `6690109900001125` / `6690109900001216` / `6690109900001315` / `6690109900001414` / `6690109000011040`(等,详见源) |
| Jaywan co-badge Mastercard 3DS | `5175540000050008` / `5175540000050099` / `5175540000050073` |
| Jaywan co-badge Visa 3DS | `4439130000050003` / `4439130000050011` / `4439130000050086` / `4439130000050094` |

## 交易响应 —— 由到期日触发(标准卡)
| 到期日 | 交易响应 (Gateway Code) |
| --- | --- |
| `01/39` | APPROVED |
| `05/39` | DECLINED |
| `04/27` | EXPIRED_CARD |
| `08/28` | TIMED_OUT |
| `01/37` | ACQUIRER_SYSTEM_ERROR |
| `02/37` | UNSPECIFIED_FAILURE |
| `05/37` | UNKNOWN |

> 注:不同 acquirer/区域段(First Data / Cielo / UK / Mexico 等)的到期日→响应映射**不完全相同**(如 First Data US 的 DECLINED 是 `05/28`、EXPIRED 是 `06/33`)。跨区域测试前核对源页对应小节。

## CSC / CVV 响应 —— 由 CSC 值触发(标准卡)
| CSC/CVV | 响应 (Gateway Code) |
| --- | --- |
| `100` | MATCH |
| `101` | NOT_PROCESSED |
| `102` | NO_MATCH |
| `1000` / `1010` / `1020`(AMEX 四位) | MATCH / NOT_PROCESSED / NO_MATCH |

## AVS 响应 —— 由账单地址街道名触发(标准卡)
| 街道名 | AVS 响应 |
| --- | --- |
| Alpha St | ADDRESS_MATCH |
| Gamma St | NOT_VERIFIED |
| November St | NO_MATCH |
| Whiskey St | ZIP_MATCH |
| X-ray St | ADDRESS_ZIP_MATCH |
| Kilo St / Oscar St / Lima St | NAME_MATCH / NAME_ADDRESS_MATCH / NAME_ZIP_MATCH |
| Sierra St / Romeo St / Uniform St / Zero St | SERVICE_NOT_SUPPORTED / SERVICE_NOT_AVAILABLE_RETRY / NOT_AVAILABLE / NOT_REQUESTED |

## Google Pay 测试卡
| 场景 | 卡组织 | 卡号 | 到期 |
| --- | --- | --- | --- |
| DPAN(设备本地卡) | Mastercard | `5513 5656 9023 3243` | 12/2039 |
| DPAN | Visa | `4005 5202 0126 4821` | 12/2029 |
| FPAN(Google 账户卡) | Mastercard | `5588 8612 7112 6256` | 12/2039 |
| FPAN | Visa | `4508 7500 1574 1019` / `4111 1111 1111 1111` | 12/2028 |

## DCC(动态货币转换)测试卡 —— 待用时查源
MPGS 提供按 **base 币种 × 目标币种** 的大量 DCC 测试卡(含 AED/QAR 等中东币种)。数据量大、随汇率更新,不在此全量落库;需要时查 `source_ref` 的 "Payment options inquiry test cards – DCC" 小节。要点:测试档案下网关会把汇率改成"保留前 2 位有效值 + 补 9"(如 MYR≈3.29999)以示测试。

## QA 关注点
- **卡号固定、结果靠字段**:同一张卡改到期日/CSC/街道名即可覆盖 approve/decline/expired/timeout/CVV/AVS 全矩阵;写用例时明确这三者的取值与预期 Gateway Code。
- **区域差异**:AstraTech 主要用 UAE(Mada/Jaywan)+ 标准段;跨区域(First Data/Cielo/UK/MX)到期日映射不同,勿套用标准段。
- **3DS**:标记 "3DS enrolled" 的卡才支持 `authentication.channel=PAYER_BROWSER` 的认证测试;详细 3DS 流程用 3DS 模拟器(见源)。
- 落库校验对应 [[tbl_acquireii_t_channel_param]](渠道返回:ISO 响应码/授权号/ECI)与 [[tbl_acquireii_t_payment_info]]。
