---
title: 通用 curl/Postman 调用骨架
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-curl-postman-templates
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2125922317
tags: []
---

# 通用 curl/Postman 调用骨架

本页给出商户收单测试中最常用的几种接口调用骨架（Header / Create Order / Refund / Get Balance / 对账单下载）。完整签名计算逻辑见 SDK 文档；测试时一般使用平台预签工具，本页示例中的 `sign` 字段为占位。环境域名与 MID 配置参见 [[merchant-acquisition-test-environment-tools]]。

## 通用 Header

所有 SGS 网关接口共用以下 Header：

```
Content-Type: application/json
Content-Language: en
sign: <RSA 私钥签名 + Base64>
Partner-Id: 200000434597
```

要点：
- `Partner-Id` 为商户 MID，按测试场景替换。
- `requestTime` 与服务端偏差 > 15 分钟会返回 `400 REQUESTTIME_TOO_EARLY/LATER`。
- `merchantOrderNo` 命名建议 `QA_<场景>_<时间戳>_<可选标记>`，详见 [[merchant-acquisition-test-data-preparation]]。

## Create Order（PAYPAGE）

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

字段要点：
- `paySceneCode` 决定收银台流程；非法值返回 `62012 PAYSCENECODE_ILLEGAL`。
- 商户未开通对应产品包返回 `62026 PRODUCT_IS_NOT_APPLIED`。
- 同一 `merchantOrderNo` 重复下单返回 `62016 MERCHANT_ORDER_NO_EXIST`。
- 错误码完整列表见 [[merchant-acquisition-error-code-cheatsheet]]。

## Refund

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

字段要点：
- `refundMerchantOrderNo` 是退款单自己的商户单号，与原单的 `originMerchantOrderNo` 解耦。
- 退款金额超过可退余额返回 `62006 REFUND_AMOUNT_EXCEEDED`。
- 已撤销 / 已退款的订单分别返回 `62040 ACQUIRE_ORDER_REVOKED` / `62041 ACQUIRE_ORDER_REFUNDED`。

## Get Balance

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

用途：核对资金流执行后商户 Basic 账户的余额变化，配合 [[merchant-acquisition-e2e-five-stage-verification]] 段 ④ Fund Flow 校验。

## 对账单下载

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
- 返回 ZIP 包含 Transaction / Settlement / Fund Statement 三类 CSV。
- `statementDate` 为 T 日；T+1 上午约 10 分钟生成，建议 30 分钟后下载。
- PreAuth 不进对账单，Capture 才进。
- 文件结构与字段含义见 [[merchant-acquisition-notify-statement-spec]]。

## 配套检查

每跑一笔 curl 调用后，按 [[merchant-acquisition-per-transaction-checklist]] 走完接口响应、服务调用链、DB 落库、Fund Flow、通知与对账五段验证，不要只看 `applyStatus=SUCCESS` 就收工。
