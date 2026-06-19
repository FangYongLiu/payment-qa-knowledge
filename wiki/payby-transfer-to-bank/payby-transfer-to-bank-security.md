---
title: PayBy转账到银行接口安全规则
domain: fund-out-transfer
kind: wiki_page
slug: payby-transfer-to-bank-security
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-transfer-tobank-v2.4-p1
tags: []
---

# PayBy转账到银行接口安全规则

本页说明 PayBy 转账到银行账户接口在传输、签名、加密层面的安全要求，以及商户侧密钥生成的操作指引。整体接入规则参见 [[payby-transfer-to-bank-overview]]。

## 协议规则

调用 API 必须遵守以下约定：

| 方式 | 说明 |
| --- | --- |
| 传输方式 | HTTPS |
| 提交方式 | POST |
| 数据格式 | JSON |
| 字符编码 | UTF-8 |
| 签名算法 | SHA256WithRSA |
| 签名要求 | 请求和响应数据都需要签名 |

## 签名算法

- 算法：`SHA256WithRSA`，私钥由商户自己颁发。
- 签名原文规则：请求 Http Body 的原始内容。
- 原文使用 UTF-8 编码。
- 签名结果使用 Base64 编码。
- 签名值通过 Http Header 中的 `sign` 字段传递；同时需在 Header 携带 `Partner-Id`（商户号）和可选的 `Content-Language`。

## 加密算法

适用于敏感字段（如 [[api_transfer_get_iban_holder_name]] 中的 `holderName`、`iban`，以及订单中标注"原文的sha256的值"的 `holderName`、`Iban`、`beneficiaryAddress` 等）：

- 算法：`RSA` 公钥加密，公钥由 PayBy 颁发。
- 加密字段不宜过大，一般不超过 200 字节。
- 加密规则：`RSA(加密原文)`。
- 明文使用 UTF-8 编码。
- 加密结果使用 Base64 编码。

## 私钥生成操作指引

商户侧推荐使用 OpenSSL 生成 RSA 密钥对（密钥大小至少 2048）：

```shell
### 生成密钥
# PayBy_key.pem    密钥文件名称
# 2048             密钥大小，至少 2048
openssl genrsa -out PayBy_key.pem 2048

### 导出公钥
# PayBy_key.pem            上一步生成的密钥文件
# PayBy_key_public.pem     导出公钥名称
openssl rsa -in PayBy_key.pem -out PayBy_key_public.pem -pubout

### 导出 Java 可用的私钥
# PayBy_key.pem            第一步生成的密钥文件
# PayBy_key_private.pem
openssl pkcs8 -in PayBy_key.pem -topk8 -nocrypt -out PayBy_key_private.pem
```

操作要点：
- 商户保留私钥用于请求签名，公钥提供给 PayBy 用于验签。
- PayBy 颁发的公钥用于商户对敏感字段做 RSA 加密。
- Java 集成场景需使用 `pkcs8` 格式的私钥。

## 请求/响应公共头

所有接口（如 [[api_transfer_get_iban_holder_name]]、[[api_transfer_get_fundout_ability_list]]）请求与响应的 Http Header 均包含：

| 字段 | 必填 | 说明 |
| --- | --- | --- |
| `Content-Language` | Optional | 文案语言，如 `en` |
| `sign` | Required | 按本页签名规则生成的签名 |
| `Partner-Id` | Required | 商户号 |
