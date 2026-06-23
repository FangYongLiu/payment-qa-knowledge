---
title: GPPC-DGPAY渠道密钥交换与配置指南
domain: channel-integration
kind: wiki_page
slug: gppc-dgpay-key-exchange-guide
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1142947906
tags: []
---

# GPPC-DGPAY渠道密钥交换与配置指南

本页说明 PayBy 与 DGPAY 对接时所需的 RSA 公私钥生成、API Token 配置，以及双方需要互相提供的凭证信息和 Key Vault 存储路径。

## 对接所需交换的凭证总览

PayBy 需提供给 DGPAY：
- Public Key 的 `Modulus` 和 `Exponent`
- API Token 的 `username` 和 `password`

DGPAY 需提供给 PayBy：
- Token `username`（`ASTRATECH`）和 `password`
- Public Key 的 `Modulus` 和 `Exponent`

DgPay 联系人：`gokhan.leblebici@dgpays.com`

## 生成 PayBy 私钥/公钥（API 公私钥）

使用 `openssl` 生成 1408 位 RSA 密钥对，并导出 Java 可用的 pkcs8 格式：

```bash
# 生成私钥：private.pem
openssl genrsa -out private.pem 1408

# 计算公钥：public.pem
openssl rsa -in private.pem -pubout -out public.pem

# 检查私钥
openssl rsa -in private.pem -check

# 转换默认格式为 pkcs8（Java 用）
openssl pkcs8 -in private.pem -topk8 -nocrypt -out private_pkcs8.pem

# 获取 public key 对应的 Modulus 和 Exponent
openssl rsa -pubin -in public.pem -text -noout -modulus
```

执行完成后即可得到私钥与公钥，需要把 public key 的 `Modulus` 和 `Exponent` 提供给 DGPAY。

## PayBy 公私钥的 Key Vault 存储

| subject | Vault Type | Vault Key |
|---|---|---|
| PayBy Public Key | Certificate | SIM: `kv-biz-sim.payby-dgpay-rsa-publickey-01`<br>UAT: `kv-biz-uat.payby-dgpay-rsa-publickey-01`<br>PROD: `kv-biz-payby-prd.payby-dgpay-rsa-publickey-01` |
| PayBy Private Key | Secret | SIM: `kv-biz-sim.payby-dgpay-rsa-privatekey-01`<br>UAT: `kv-biz-uat.payby-dgpay-rsa-privatekey-01`<br>PROD: `kv-biz-payby-prd.payby-dgpay-rsa-privatekey-01` |

## DGPAY 集成配置

DgPay 提供 token 的 `username`、`password` 与 public key（`Modulus`、`Exponent`），其中 password 与 public key 信息需存储到 Key Vault。

| subject | key | value | Vault Type | Vault Key |
|---|---|---|---|---|
| DGPAY TOKEN | username | `ASTRATECH` | - | - |
| DGPAY TOKEN | password | already provided by dgpay | Secret | SIM: `kv-biz-sim.3rddgpay-http-password-01`<br>UAT: `kv-biz-uat.3rddgpay-http-password-01`<br>PROD: `kv-biz-3rddgpay-prd.3rddgpay-http-password-01` |
| Public Key | Modulus | already provided by dgpay | Secret | SIM: `kv-biz-sim.3rddgpay-publickey-modulus-01`<br>UAT: `kv-biz-uat.3rddgpay-publickey-modulus-01`<br>PROD: `kv-biz-3rddgpay-prd.3rddgpay-publickey-modulus-01` |
| Public Key | Exponent | already provided by dgpay | Secret | SIM: `kv-biz-sim.3rddgpay-publickey-exponent-01`<br>UAT: `kv-biz-uat.3rddgpay-publickey-exponent-01`<br>PROD: `kv-biz-3rddgpay-prd.3rddgpay-publickey-exponent-01` |

## 生成 PayBy API Token 用户名/密码

PayBy 侧需自行生成 API Token 的 username 和 password，并提供给 DGPAY；password 存入 Key Vault。

| subject | key | value | Vault Type | Vault Key |
|---|---|---|---|---|
| PAYBY TOKEN | username | SIM: `sim-payby-dgpay`<br>UAT: `uat-payby-dgpay` | - | - |
| PAYBY TOKEN | password | - | Secret | SIM: `kv-biz-sim.payby-dgpay-http-password-01`<br>UAT: `kv-biz-uat.payby-dgpay-http-password-01`<br>PROD: `kv-biz-payby-prd.payby-dgpay-http-password-01` |

## 提供给 DGPAY 的信息清单

需要把以下两类信息发送给 DGPAY：

- Public Key 的 `Modulus` 和 `Exponent`（从「生成 PayBy 私钥/公钥」步骤产出）
- API Token 的 `username` 和 `password`（从「生成 PayBy API Token」步骤产出）

> TODO：参考 `ppc-运营-1-证书交换`。
