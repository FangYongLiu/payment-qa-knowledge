---
id: domain_payby_acquire_transaction
object_type: Domain
domain: payby-acquire-transaction
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki_attachment
source_ref: wiki_attachment:1d3b3713-3d92-4fd2-a760-42f5f4e3a4b6
tags:
- payby
- acquire
- payment
- refund
subdomain: null
module: null
sensitivity: normal
name: PayBy收单交易
aliases: []
related_services: []
related_tables: []
related_scenarios:
- payby-acquire-payment-scenarios
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
PayBy收单交易业务域涵盖商户系统通过 PayBy 支付系统完成在线/线下交易闭环所需的能力集合，包括下单（创建订单）、支付、退款、查询、取消、冲正、分账、对账、更新订单超时时间等。该域的接口与业务对象由商户系统（在线购物平台、人工收银、自动化收银等）通过 HTTPS + POST + JSON + UTF-8 + SHA256WithRSA 签名规则与 PayBy 支付系统交互。

## 覆盖范围
- 创建订单（PlaceAcquireOrder）：支持多支付场景下单，关键请求/返回字段见 AcquireOrder。
- 支付：通过 paySceneCode 与 paySceneParams、interactionParams 驱动多种支付场景完成支付。
- 退款（PlaceRefundOrder）：支持金额退款、分账退款（refundSharingAmount、sharingParamList）、代扣代缴退款（withholdAndRemitFee）等。
- 查询：查询订单、查询退款订单、查询卡信息、解绑卡、查询收银台 URL 信息、查询会员余额。
- 取消订单（CancelOrder）：通过 merchantOrderNo 或 orderNo 取消未支付订单。
- 冲正（Revoke）：对已支付订单进行冲正，AcquireOrder.revoked = true 表示冲正成功。
- 更新订单超时时间（UpdateExpiredTime）。
- 分账：创建订单与退款订单中的 sharingParamList、sharingInfoList、sharingSettledFeeAmount、withholdAndRemitFee、sharingRemainRefundInfoList。
- 对账：下载对账单接口（资金对账单接口已于 v2.0.19 删除）。
- 通知：支付结果通知、退款结果通知。
- 出款（与本域相关的关联接口，仅作为接口总览出现）：单笔付款到账户、单笔付款到银行卡及其查询、商户付款成功通知（属外延，不属本域核心收单）。

## 关键服务/流程
- 协议规则：传输 HTTPS、提交 POST、数据 JSON、编码 UTF-8、签名 SHA256WithRSA，请求/响应均需签名；空值请求参数不予处理。
- 支付场景代码 paySceneCode：JSAPI / INAPP / PAYPAGE / DYNQR / QRPAY / AUTODEBIT / CASHTOPUP / FACE / DIRECTPAY / EWALLET / PAYANDSIGN。
- 场景参数与交互参数：通过 paySceneParams（如 payerMid、authCode、authProtocolNo、authToken、cardNo/cardToken、redirectUrl、oneTimePayment、customerId、protocolSceneCode 等）与 interactionParams（tokenUrl、threeDSecureDom、installmentUrl、deepLink）驱动具体支付路径。
- 关键数据对象：AcquireOrder、PaymentInfo、CardInfo、ChannelParam、Money、AccessoryContent（AmountDetail/GoodsDetail/TerminalDetail）、SharingInfo、PromotionInfo、RefundOrder、RefundSummary、TransferOrder、TransferToBankOrder。
- 状态：AcquireOrderStatus（订单状态），退款订单状态包含 REFUNDED_SETTLED 等。
- 货币：currency 当前示例为 AED。
- 商户订单号 merchantOrderNo：字母/数字/中划线/下划线，长度 32（退款商户订单号 64），需保持唯一；已支付或已取消的订单号不能重新发起支付；重新发起未完成支付须沿用原订单号避免重复支付。
- tokenUrl 有效期 1 小时，超时需用相同业务参数重新创建订单。
- expiredTime 上限调整至 48 小时（v2.4）。
- 冲正应用场景：参考查询订单的冲正描述（v2.0.16）。
- DIRECTPAY：支持首次支付（cardNo/holderName/cvv/expYear/expMonth/saveCard 等）、savedCard 支付（cardToken）、分期支付（type=INSTALLMENT、uniqueId、installmentUrl）。
- 3DS：threeDSecure 由商户传入，但风控判断结果优先于商户要求。
- EWALLET：eWalletCode 支持 payby/botim-pay/ALIPAYPLUS/WECHATPAY（WECHATPAY 需安装 WECHAT SDK）。
- PAYANDSIGN：通过 protocolSceneCode、protocolNotifyUrl、customerId 完成支付并签约。

## QA 关注点
- 协议合规：HTTPS/POST/JSON/UTF-8/SHA256WithRSA 签名校验；空请求参数被忽略的处理。
- 商户订单号唯一性：重复支付、已支付/已取消订单不可再发起支付的拦截校验；merchantOrderNo（32）、refundMerchantOrderNo（64）长度边界。
- tokenUrl 1 小时过期、expiredTime 48 小时上限、UpdateExpiredTime 接口的边界。
- paySceneCode 与 paySceneParams/interactionParams 的匹配关系（必填/可填差异），oneTimePayment=true 时支付失败将订单置失败的行为验证。
- DIRECTPAY 加密字段（cardNo/holderName/cvv）传输与 saveCard、cardToken 复用流程；cardNo 与 cardToken 同时传入时以 cardToken 推进。
- 3DS：商户 threeDSecure 与风控判定优先级；threeDSecureDom/installmentUrl 返回正确性。
- 冲正：AcquireOrder.revoked 状态；冲正接口返回码 62046；冲正与查询订单的关联场景。
- 退款：分账退款 refundSharingAmount/sharingParamList、feeRefunded、sharingRemainRefundInfoList、withholdAndRemitFee 的金额一致性。
- 分账：sharingInfoList、sharingSettledFeeAmount、withholdAndRemitFee 字段一致性。
- 对账：下载对账单接口（v2.0.19 后仅保留交易对账单）的文件名/格式校验。
- 关键返回码覆盖：62001（取消订单/退款返回码调整）、62035-62038、62040、62042-62049、62065、62073、62078、62080、62081、62083、62084、62085、62087、62088 等的触发条件与文案。
- 通知：支付结果/退款结果通知参数（v2.8 调整）的签名校验、重试与幂等。
- 货币与金额：Money(amount Decimal(12,2), currency AED) 边界与精度。
- 字段长度边界：subject 200、product 200、payee
