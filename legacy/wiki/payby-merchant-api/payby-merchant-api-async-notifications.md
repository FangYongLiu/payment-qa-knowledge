---
title: PayBy异步通知机制总览
domain: payby-open-api
kind: wiki_page
slug: payby-merchant-api-async-notifications
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p17
tags: []
---

# PayBy异步通知机制总览

PayBy 在订单状态变化或资金事件发生时，会以数据流形式向商户后台推送异步通知，商户需按统一规范接收处理并应答。本页汇总各类异步通知的统一规则、重试策略、应答格式与各通知的参数定义。

## 通用规则

- **重复通知**：同一通知可能多次发送给商户系统，商户系统必须能够正确处理重复通知（幂等处理）。
- **失败重试**：当 PayBy 收到的应答不符合规范或超时，将判定本次通知失败并重新发送，直到成功为止；但 PayBy 不保证通知最终一定成功。
  - 默认重试 **7 次**，时间间隔（单位：分钟）：**2, 10, 10, 60, 120, 360, 900**。
- **兜底建议**：在订单状态不明或未收到通知时，建议商户主动调用查订单接口确认状态；对账可使用 [[payby-merchant-api-statement-download]]。

## 统一应答格式

商户收到任意通知后，需返回：

```json
{"response":"SUCCESS"}
```

返回该值表示成功接收，其他任意内容均视为异常并触发重试。

## 支付结果通知

支付成功后，PayBy 将支付结果与用户信息推送给商户。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 订单信息 | acquireOrder | Required | AcquireOrder |

适用通用重复通知与 7 次重试策略；订单状态不明时建议主动查询订单。

## 退款结果通知

商户申请的退款产生结果后，PayBy 推送退款结果。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 退款订单信息 | refundOrder | Required | RefundOrder |

适用通用重复通知与 7 次重试策略。

## 商户付款到账户成功通知

商户付款到账户、且收款账户实际收到资金后，PayBy 推送结果。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 付款到账户订单信息 | payToBalanceOrder | Required | RefundOrder |

## 商户付款到银行卡成功通知

商户付款到银行卡产生结果后，PayBy 推送结果。具体到账时间取决于各银行的结算时间，以实际到账时间为准。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 付款到银行卡订单信息 | payToCardOrder | Required | PayToCardOrder |

## 拒付通知

发生拒付（Chargeback）后，PayBy 推送拒付信息。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 拒付订单 | acquireChargeback | Required | AcquireChargeback |

适用通用重复通知与 7 次重试策略；订单状态不明时建议主动查询订单。

## VAM 充值通知

发生 VAM 充值时，PayBy 推送充值信息（详见 [[api_payby_notify_vam_deposit]]）。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 充值订单 | vamDepositOrder | Required | VamDepositOrder |

通知样例：

```json
Http Header
{
    "Content-Type": "application/json; charset=UTF-8"
}

Http Body
{
    "notify_time": "20241224061738",
    "vamDepositOrder": {
        "remitterInfo": "MR HUA JIANG",
        "amount": {
            "amount": 3000,
            "currency": "AED"
        },
        "orderNo": "131727701521486397",
        "referenceNo": "UFOC0HQ008",
        "senderBankCode": "BBMEAEADXXX",
        "depositDetails": "REF AEV260832YLQ4K5D FIS 56057df891a0449584dc5c8d84a6a138",
        "transactionTime": 1727701521000,
        "status": "SUCCESS"
    },
    "_input_charset": "UTF-8",
    "notify_timestamp": 1735006658869,
    "notify_id": "202409300013926551"
}
```

适用通用重复通知与 7 次重试策略；订单状态不明时建议主动查询订单。

## 通知类型与参数对象一览

| 通知类型 | 参数变量名 | 参数类型 |
| --- | --- | --- |
| 支付结果通知 | acquireOrder | AcquireOrder |
| 退款结果通知 | refundOrder | RefundOrder |
| 付款到账户成功通知 | payToBalanceOrder | RefundOrder |
| 付款到银行卡成功通知 | payToCardOrder | PayToCardOrder |
| 拒付通知 | acquireChargeback | AcquireChargeback |
| VAM 充值通知 | vamDepositOrder | VamDepositOrder |
