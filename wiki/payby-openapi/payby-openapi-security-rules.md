---
title: PayBy开放接口安全规则(签名与加密)
domain: payby-openapi
kind: wiki_page
slug: payby-openapi-security-rules
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p8
tags: []
---

# PayBy开放接口安全规则(签名与加密)

本页说明 PayBy OpenAPI 在请求交互中使用的签名与加密规则，包括算法选择、编码方式以及密钥生成的建议命令。

## 签名算法

- 算法：`SHA256WithRSA`
- 私钥：由商户自己颁发并保管
- 签名原文：请求 Http Body 的原始内容
- 原文编码：UTF-8
- 签名结果编码：Base64

## 加密算法

- 算法：`RSA` 公钥加密，公钥由 PayBy 颁发
- 加密字段大小限制：一般不超过 200 字节
- 加密规则：`RSA(加密原文)`
- 明文编码：UTF-8
- 加密结果编码：Base64

## 密钥生成建议

商户可使用 OpenSSL 生成签名所需的 RSA 密钥对，密钥大小至少 2048 位。

### 生成密钥

```shell
# PayBy_key.pem   密钥文件名称
# 2048            密钥大小，至少 2048
openssl genrsa -out PayBy_key.pem 2048
```

### 导出公钥

```shell
# PayBy_key.pem            上一步生成的密钥文件
# PayBy_key_public.pem     导出公钥名称
openssl rsa -in PayBy_key.pem -out PayBy_key_public.pem -pubout
```

### 导出 Java 可用的私钥

```shell
# PayBy_key.pem             第一步生成的密钥文件
# PayBy_key_private.pem     PKCS8 格式私钥
openssl pkcs8 -in PayBy_key.pem -topk8 -nocrypt -out PayBy_key_private.pem
```

## 要点速查

| 用途 | 算法 | 密钥来源 | 编码 |
|---|---|---|---|
| 签名 | SHA256WithRSA | 商户自有私钥 | UTF-8 原文 / Base64 签名 |
| 加密 | RSA | PayBy 颁发公钥 | UTF-8 明文 / Base64 密文 |
