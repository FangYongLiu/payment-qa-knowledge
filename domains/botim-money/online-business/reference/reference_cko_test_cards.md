---
id: reference_cko_test_cards
object_type: Reference
name: CKO 渠道官方测试卡 (Checkout.com Test Cards)
aliases: [CKO test cards, checkout.com test cards, CKO 测试卡]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
source_type: reference
source_ref: 'https://www.checkout.com/docs/developer-resources/testing/test-cards (fetched 2026-07-03)'
tags: [online-business, 收单, CKO, checkout, 测试卡, test-card, card-payment]
related_services: [svc_acquireii, svc_qpay_cko]
related_scenarios: [scn_online_business_mpgs_channel, scn_cko_subscription_payment]
---

# CKO 渠道官方测试卡 (Checkout.com Test Cards)

商户收单卡支付测试用的 **Checkout.com(CKO)官方测试卡**。用于 [[svc_qpay_cko]] 渠道、[[svc_acquireii]] 收单核心的卡支付/3DS/退款/代付测试。

> **仅 sandbox 使用,禁止用真实卡。** 测试支付时:卡号取下表 + 目标响应码;CVV 任意 3 位(Amex 4 位);到期日任意未来日期(MM/YY 或 MM/YYYY)。sandbox 支付保留 30 天。
> **3DS challenge 模拟器密码:`Checkout1!`**。数据源见 frontmatter `source_ref`。

## 默认卡(模拟成功/失败)
| 类型 | 卡号 | 响应码 | 国家 |
| --- | --- | --- | --- |
| Credit | `4242424242424242` | 10000(成功) | GB |
| Credit | `4242424242424242`(金额设为 101) | 20051(余额不足) | GB |
| Credit | `4000020000000000` | 10000 | US |
| Credit | `4273149019799094`(仅卡校验;Capture/Void 会被拒) | 10000 | TR |
| Debit | `4659105569051157` | 10000 | GB |
| Prepaid | `4000148147058142` | 20020 | – |

## 响应码测试卡(触发指定 API 响应码)
| 响应码 | 说明 | Visa 卡号 | 国家 |
| --- | --- | --- | --- |
| 20001 | Refer to card issuer | `4111111111111129` | US |
| 20012 | Invalid transaction | `4024007103573027` / `4158596042924182` | US/GB |
| 20014 | Invalid card number | `4485381577182090` | US |
| 20051 | Insufficient funds | `4544249167673670` | GB |
| 20057 | Not permitted to cardholder | `4659465888705671`(AFT) / `4151512736305999`(非AFT) | GB |
| 20059 | Suspected fraud | `4897453568485113` / `4000144348235050`(prepaid) | US |
| 20061 | Activity amount limit exceeded | `4556294593757189` | UY |
| 20062 | Restricted card | `4818924250131070` | GB |
| 20063 | Security violation | `4556253752712245` | US |
| 20068 | Late/timeout/rejected/internal error | `4095254802642505` | US |
| 20154 | 3DS authentication required | `4500622868341387` | CA |
| 2005C | Not supported / blocked by issuer | `4276038578596818` | US |
| 2009G | Blocked by cardholder | `4152812521833588` | US |
| 200N7 | Decline for CVV2 failure | `4734868958733862` | US |
| 30015 | No such issuer | `4024007162185267` / `4655710037275959` | US/GB |
| 30041 | Lost card – pick up | `4941202060999329` / `4658620059821613` | GB |
| 30043 | Stolen card – pick up | `4539253655711767` / `4745820750643143` | IE/GB |

## 3DS 测试卡(代表卡;全表见源)
**3DS2 frictionless(无挑战)** —— 结果由卡号决定:
| 结果 | 卡组织 | 卡号 |
| --- | --- | --- |
| Authentication successful | Visa / Mastercard / Amex | `4485040371536584` / `5588686116426417` / `345678901234564` |
| Not authenticated | Visa / Amex | `4539628347117863` / `371064645462927` |
| Authentication rejected | Amex / Visa | `343397288296672` / `4275765574319271` |
| Card not enrolled | Visa / Amex | `4484070000035519` / `378282246310005` |

**3DS2 challenge(挑战流,模拟器密码 `Checkout1!`)**:
| 结果 | 卡组织 | 卡号 |
| --- | --- | --- |
| Authentication successful | Amex / Mastercard / Visa | `372688581899681` / `5385308360135181` / `4010061700000021` |
| Authentication attempted | Visa / Amex | `4152868552773614` / `346126139326850` |
| Authentication rejected | Amex / Visa | `375982239796002` / `4150561000000019` |
| Not authenticated | Visa / Mastercard | `4243754271700719` / `5258901507741160` |

**非 3DS 卡**(请求 `3ds.enabled: true` 时返回 20150 "Card not 3D-Secure enabled"):
`3530111333300000`(JCB, CVV 100) / `5352151570003404`(MC Debit, 100) / `4532432452900131`(Visa, 257)

## 卡校验(amount=0 成功;amount>0 授权按响应码拒)
| 卡号 | 响应码 | 说明 |
| --- | --- | --- |
| `4644968546281686` / `5355228287185489` | 20012 | Invalid transaction |
| `4546381219393284` / `5355229757805879` / `4325350188287824` | 20051 | Insufficient funds |
| `4543611423334994` / `5355222589678168` / `4394666298116207` | 20061 | Activity amount limit |
| `4857662623668665` / `5355225201525238` / `4021277034700287` | 20062 | Restricted card |
| `4407108123937239` / `5355226042898974` | 20063 | Security violation |

## 增量授权(仅 Visa 信用卡,模拟拒绝)
| 卡号 | 响应码 | 错误码 |
| --- | --- | --- |
| `4659959652550685` | – | incremental_authorization_unsupported |
| `4446900535698356` | – | incremental_authorization_restricted_for_mcc |
| `4140253846048187` | 20005 | – |
| `4556447238607884` | 20068 | – |

## 过期支付工具(创建时设过去到期日 → 20054;更新未来到期日 → 10000)
Visa Debit `4532446037926437` / prepaid `4000141680788456` / Mastercard Debit `5287286878576972`。

## 代付测试卡(Card Payout,消费者借记卡)
| 响应码 | 卡号 |
| --- | --- |
| 10000(成功) | `4921817844445119`(GB) / `4978313915783283`(FR) / `4076613139850359`(SG) / `4024764449971519`(US) |
| 20005 | `4818192525595285`(GB) / `4558473893020179`(FR) / `4811553373235190`(SG) / `4610179846730147`(US) |
| 20057 | `4818192160565981`(GB) / `4975992266555193`(FR) / `4815649658513826`(SG) / `4610174464118832`(US) |

## QA 关注点
- **成功码 10000、失败码 2xxxx/3xxxx**:响应码测试卡是覆盖拒付/欺诈/风控分支的主力;卡校验类用 amount 控制成功/拒。
- **3DS**:frictionless 结果由卡号决定;challenge 流会跳模拟器,密码 `Checkout1!`;非 3DS 卡在 `3ds.enabled:true` 下返回 20150。本页所有卡也可当有效 network token 用。
- **金额触发**:默认卡 `4242…4242` 金额设 101 → 20051,可快速造"余额不足"。
- 落库校验对应 [[tbl_acquireii_t_channel_param]] 与 [[tbl_acquireii_t_payment_info]];3DS 结果参考 compliance 库 `t_event_3ds_result`。
- 全量 3DS 卡表(每种结果多卡组织)随源更新,需要时查 `source_ref`。
