---
id: api_payby_transfer_to_bank_notify
object_type: API
domain: wallet
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-tobank-v2.4-p3
tags:
- notify
- callback
- transfer-to-bank
subdomain: null
module: null
sensitivity: normal
name: 商户付款到银行卡成功通知
aliases: []
related_services:
- svc_transfer
---

## 用途
当商户付款到银行卡有结果后,PayBy 把相关结果异步推送给商户,商户需要接收处理并返回应答。具体到账时间因各银行结算时间不同，以具体到账时间为准。

注意事项：
1. 同一个通知可能会被多次发送到商户系统,商户系统必须能够正确处理重复通知(幂等)。
2. 若 PayBy 收到的商家响应不符合规范或超时,PayBy 将判定通知失败并重新发送,直到成功。默认重试 7 次,时间间隔(分钟)：2、10、10、60、120、360、900。但 PayBy 不保证通知最终一定成功。
3. 若订单状态不明或未收到通知,建议商户主动调用转账查询接口确认订单状态(参见 [[api_payby_get_transfer_to_bank_order]])。
4. 通知请求需要签名,签名算法与普通请求相同。消息由 PayBy RSA 私钥签署,商户应使用从商户 portal 下载的 PayBy 公钥验证签名。

## 路径/方法
- 协议: HTTP
- 方法: POST(由 PayBy 主动回调商户的 notifyUrl)
- 目标地址: 商户在下单时提供的 notifyUrl
- Content-Type: application/json; charset=UTF-8

## 入参
Http Header:
- Content-Type: application/json; charset=UTF-8

Http Body(JSON 对象,与普通请求格式相同):

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|---|
| 字符集 | _input_charset | - | String | 例: UTF-8 |
| 通知 ID | notify_id | - | String | 例: 202004140007474501 |
| 通知时间 | notify_time | - | String | 例: 20200414113800 |
| 付款到银行卡订单信息 | transferToBankOrder | Required | TransferToBankOrder | - |

TransferToBankOrder 主要字段(示例)：
- amount.amount, amount.currency
- holderName(脱敏)
- iban(脱敏)
- memo
- merchantOrderNo
- notifyUrl
- orderNo
- paymentInfo.arrivalTime
- paymentInfo.payerFeeAmount.amount / currency
- product (例: "Transfer To Bank")
- requestTime
- status (例: SUCCESS)
- swiftCode

## 出参
商户收到通知后,需在 HTTP 响应体中返回字符串 `SUCCESS` 表示成功接收;返回其他内容均表示异常,PayBy 将按重试策略再次推送。

## 错误码
本接口为 PayBy → 商户的回调,无业务返回码。商户响应规则：
- 返回 `SUCCESS`：PayBy 视为成功,停止重试。
- 返回非 `SUCCESS` 或超时/不符合规范：PayBy 视为失败,按默认 7 次、间隔 2/10/10/60/120/360/900 分钟重试。

## 测试校验点
1. 签名校验：使用 PayBy 公钥验证 Header `Sign`,签名算法与普通请求一致。
2. 幂等性：相同 notify_id / merchantOrderNo / orderNo 多次到达,商户业务结果一致,不重复入账。
3. 应答规范：仅当成功处理后返回字符串 `SUCCESS`,其它情况返回非 SUCCESS,验证 PayBy 触发重试。
4. 重试策略：模拟商户超时或返回非 SUCCESS,校验重试次数=7、间隔为 2、10、10、60、120、360、900 分钟。
5. 状态一致性：通知中的 status=SUCCESS 与 [[api_payby_get_transfer_to_bank_order]] 查询结果一致(amount、currency、merchantOrderNo、orderNo、arrivalTime、swiftCode 等)。
6. 字段完整性：transferToBankOrder 必填字段(merchantOrderNo、orderNo、status、amount、product、requestTime)存在且类型正确。
7. 敏感字段：holderName、iban 在通知中以脱敏(加密)形式呈现,与下单/查询保持一致。
8. notifyUrl 不可达/异常时,PayBy 仍按重试策略推送;商户最终未成功接收时,需通过查询接口主动对账。
9. swiftCode 在通知样例中可能含空格(如 "BBME AEAD"),需兼容解析。
10. payerFeeAmount.currency 字段(示例中为 "D")需按实际值容错处理。
