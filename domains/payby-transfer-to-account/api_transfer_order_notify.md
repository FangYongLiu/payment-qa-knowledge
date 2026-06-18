---
id: api_transfer_order_notify
object_type: API
domain: payby-transfer-to-account
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-v1.1-p1
tags:
- notify
- async
- transfer
subdomain: null
module: null
sensitivity: normal
name: 商户付款到账户成功通知 (transferOrder Notify)
aliases:
- transferOrder Notify
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当商户付款到账户、收款账户收到钱后，PayBy 会把相关结果异步通知给商户。商户需接收处理并返回应答。通知的目标地址为商户在 placeTransferOrder 请求中传入的 `notifyUrl`。

## 路径/方法
- 路径：商户在 `placeTransferOrder` 请求参数 `notifyUrl` 中提供的商户接收通知地址。
- 提交方式：POST
- 传输方式：HTTPS
- 数据格式：JSON
- 字符编码：UTF-8
- 签名算法：SHA256WithRSA（请求和响应数据都需要签名）

## 入参
通知 Body 字段：

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 付款到账户订单信息 | transferOrder | Required | TransferOrder | 付款到账户订单 |

TransferOrder 关键字段（来自公共定义）：
- requestTime：Timestamp(3)，请求时间
- merchantOrderNo：String(64)，商户订单号
- orderNo：String(32)，PayBy 订单号
- product：String(200)，产品名称（如 Transfer）
- status：订单状态（CREATED / SUCCESS / FAILURE）
- paymentInfo：TransferPaymentInfo（payerFeeAmount、arrivalTime）
- amount：Money
- beneficiaryIdentityType：PHONE_NO / MEMBER_ID / TOTOK_UID
- beneficiaryIdentity：收款人标识（加密后传输；原文 sha256 后值返回）
- beneficiaryFullName：收款方姓名（可选）
- memo：付款备注
- notifyUrl：后台通知地址
- failCode / failDes：订单失败原因（可选，详见附录订单错误原因代码）

## 出参
商户收到通知后，需返回字符串 `SUCCESS` 表示成功接收；其他任何返回值表示异常。

## 错误码
本通知接口本身无返回码列表；商户应答仅区分：
- `SUCCESS`：成功接收
- 其他：异常（PayBy 视为未成功接收）

订单失败原因通过 `failCode`/`failDes` 携带，具体见附录订单错误原因代码。

## 测试校验点
1. 通知到达商户 `notifyUrl`，请求方式为 POST，Body 为 JSON 且 UTF-8 编码。
2. 通知请求带签名，签名算法为 SHA256WithRSA，原文为 Http Body 原始内容、Base64 编码；商户需验签通过。
3. `transferOrder.status` 为 SUCCESS 时表示付款到账户成功；FAILURE 时应携带 `failCode`、`failDes`。
4. `transferOrder.merchantOrderNo` 与 `orderNo` 与下单（placeTransferOrder）/查询（getTransferOrder）一致。
5. `beneficiaryIdentity`、`beneficiaryFullName` 在通知中以加密/sha256 形式返回，校验格式与下单时一致。
6. `paymentInfo.arrivalTime`（PayBy 付款成功时间）和 `payerFeeAmount` 在 SUCCESS 时正确返回。
7. 商户成功处理后必须返回字符串 `SUCCESS`；返回其他内容时应验证 PayBy 行为（视为异常）。
8. 商户接口需具备幂等处理能力，避免重复通知造成重复入账。
