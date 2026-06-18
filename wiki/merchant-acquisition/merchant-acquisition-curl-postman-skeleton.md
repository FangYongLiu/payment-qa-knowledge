---
title: 商户收单通用curl/Postman骨架
domain: merchant-acquisition
kind: wiki_page
slug: merchant-acquisition-curl-postman-skeleton
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:4ef3640b-38b5-4756-81d5-d729c241dc79
tags: []
---

# 商户收单通用curl/Postman骨架

本页汇总商户收单接口调试时常用的 curl 请求骨架，包含通用 Header、下单（PAYPAGE）、退款、查余额、对账单下载示例。完整签名计算逻辑见 SDK 文档；测试时一般用平台预签好的工具调用。

## 通用 Header

所有商户收单接口都需要带以下 Header：

```
Content-Type: application/json
Content-Language: en
sign: <RSA 私钥签名 + Base64>
Partner-Id: 200000434597
```

- `Partner-Id`：测试 MID，根据具体测试任务替换
- `sign`：对请求体做 RSA 私钥签名后 Base64 编码
- 时间戳偏差超过 15 分钟会触发 `400 REQUESTTIME_TOO_EARLY/LATER`

> 完整 MID 与签名密钥配置见 [[merchant-acquisition-test-environment-and-tools]]。

## Create Order（PAYPAGE）

下单接口示例（PAYPAGE 收银台模式）：

```bash
curl -X POST https://uat.test2pay.com/sgs/api/acquire2/placeOrder \
  -H "Content-Type: application/json" \
  -H "sign: <签名>" \
  -H "Partner-Id: 200000434597" \
  -d '{
    "requestTime": 1714478400000,
    "bizContent": {
      "merchantOrderNo": "QA_PAYPAGE_1714478400_3892",
      "subject": "[QA] paypage test",
      "totalAmount": { "amount": 10.00, "currency": "AED" },
      "paySceneCode": "PAYPAGE",
      "paySceneParams": {
        "redirectUrl": "https://webhook.site/your-id"
      },
      "notifyUrl": "https://webhook.site/your-id"
    }
  }'
```

要点：
- `merchantOrderNo` 命名规范见 [[merchant-acquisition-test-data-conventions]]
- `notifyUrl` 推荐用 webhook.site 接收异步通知
- 响应中 `interactionParams.tokenUrl` 是收银台跳转地址

## Refund

退款接口示例（部分退款）：

```bash
curl -X POST https://uat.test2pay.com/sgs/api/acquire2/refund/placeOrder \
  -H "Content-Type: application/json" \
  -H "sign: <签名>" \
  -H "Partner-Id: 200000434597" \
  -d '{
    "requestTime": 1714478400000,
    "bizContent": {
      "refundMerchantOrderNo": "QA_REFUND_1714478500",
      "originMerchantOrderNo": "QA_PAYPAGE_1714478400_3892",
      "amount": { "amount": 5.00, "currency": "AED" },
      "reason": "[QA] partial refund test"
    }
  }'
```

要点：
- `refundMerchantOrderNo`：本次退款单号（商户侧唯一）
- `originMerchantOrderNo`：原收单订单号
- 退款超额返回 `62006 REFUND_AMOUNT_EXCEEDED`，更多见 [[merchant-acquisition-error-code-quickref]]

## Get Balance

查询商户余额：

```bash
curl -X POST https://uat.test2pay.com/sgs/api/member/getBalance \
  -H "Content-Type: application/json" \
  -H "sign: <签名>" \
  -H "Partner-Id: 200000434597" \
  -d '{
    "requestTime": 1714478400000,
    "bizContent": { "currencyCode": "AED" }
  }'
```

常用于校验清算后的 Merchant Basic 账户余额变化。

## 对账单下载

下载 T+1 日对账单 ZIP：

```bash
curl -X POST https://uat.test2pay.com/sgs/api/acquire2/download/getOrderStatement \
  -H "Content-Type: application/json" \
  -H "sign: <签名>" \
  -H "Partner-Id: 200000434597" \
  -o "statement_$(date +%Y%m%d).zip" \
  -d '{
    "requestTime": 1714478400000,
    "bizContent": { "statementDate": "20260429" }
  }'
```

要点：
- `statementDate` 格式 `YYYYMMDD`，传昨日日期
- T+1 上午约 10 分钟生成，建议 30 分钟后下载
- ZIP 内含 Transaction / Settlement / Fund 三类 CSV，结构详见 [[merchant-acquisition-notify-and-statement]]
- PreAuth 不进对账单，Capture 才进

## 调试小贴士

- 拿到响应后先看 `head.applyStatus` 和 `head.code`，再看 `body`
- 失败响应里的 `traceCode` 可在 Kibana 全链路检索
- 跑完一笔交易请按 [[merchant-acquisition-per-transaction-checklist]] 逐项核对，不要只看接口响应

> 本页只列骨架；完整的方法论请回到 [[merchant-acquisition-test-methodology-overview]]，业务域全景见 [[domain_merchant_acquisition]]。
