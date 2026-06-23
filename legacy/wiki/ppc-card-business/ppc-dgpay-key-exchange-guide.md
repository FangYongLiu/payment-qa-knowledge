---
title: PPC-DGPAY密钥交换与集成配置指南
domain: ppc-card-business
kind: wiki_page
slug: ppc-dgpay-key-exchange-guide
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:8bcc5af4-0a0a-43ef-b978-96845d6a6982
tags: []
---

# PPC-DGPAY密钥交换与集成配置指南

本页汇总 PayBy 与 DGPAY 集成所需的 RSA 密钥生成命令、Token/公钥的 Key Vault 存储路径，以及双方需要交换的凭证清单。

## 生成 PayBy RSA 公私钥

使用 openssl 生成 1408 位 RSA 密钥对，并转换为 Java 可用的 pkcs8 格式：

```bash
# 生成私钥：private.pem
openssl genrsa -out private.pem 1408

# 计算公钥：public.pem
openssl rsa -in private.pem -pubout -out public.pem

# 检查私钥
openssl rsa -in private.pem -check

# 转换默认格式为 pkcs8 (Java 用)
openssl pkcs8 -in private.pem -topk8 -nocrypt -out private_pkcs8.pem

# 获取 publickey 对应 Modulus 和 Exponent
openssl rsa -pubin -in public.pem -text -noout -modulus
```

执行后得到私钥与公钥；需要将公钥的 **Modulus** 和 **Exponent** 提供给 DGPAY。

## PayBy 密钥的 Key Vault 存储

| Subject | Vault Type | Vault Key |
|---|---|---|
| PayBy Public Key | Certificate | SIM: `kv-biz-sim.payby-dgpay-rsa-publickey-01`<br>UAT: `kv-biz-uat.payby-dgpay-rsa-publickey-01`<br>PROD: `kv-biz-payby-prd.payby-dgpay-rsa-publickey-01` |
| PayBy Private Key | Secret | SIM: `kv-biz-sim.payby-dgpay-rsa-privatekey-01`<br>UAT: `kv-biz-uat.payby-dgpay-rsa-privatekey-01`<br>PROD: `kv-biz-payby-prd.payby-dgpay-rsa-privatekey-01` |

注意 Public Key 以 Certificate 类型存储，Private Key 以 Secret 类型存储。

## DGPAY 侧凭证配置

DGPAY 提供 token 用户名/密码与公钥（Modulus、Exponent），PayBy 侧将其密码与公钥信息存入 Key Vault。

### DGPAY TOKEN

| Key | Value | Vault Type | Vault Key |
|---|---|---|---|
| username | `ASTRATECH` | - | - |
| password | already provided by dgpay | Secret | SIM: `kv-biz-sim.3rddgpay-http-password-01`<br>UAT: `kv-biz-uat.3rddgpay-http-password-01`<br>PROD: `kv-biz-3rddgpay-prd.3rddgpay-http-password-01` |

### DGPAY Public Key

| Key | Value | Vault Type | Vault Key |
|---|---|---|---|
| Modulus | already provided by dgpay | Secret | SIM: `kv-biz-sim.3rddgpay-publickey-modulus-01`<br>UAT: `kv-biz-uat.3rddgpay-publickey-modulus-01`<br>PROD: `kv-biz-3rddgpay-prd.3rddgpay-publickey-modulus-01` |
| Exponent | already provided by dgpay | Secret | SIM: `kv-biz-sim.3rddgpay-publickey-exponent-01`<br>UAT: `kv-biz-uat.3rddgpay-publickey-exponent-01`<br>PROD: `kv-biz-3rddgpay-prd.3rddgpay-publickey-exponent-01` |

## PayBy API Token 用户名/密码

PayBy 侧生成给 DGPAY 调用的 API Token：

| Key | Value | Vault Type | Vault Key |
|---|---|---|---|
| username | SIM: `sim-payby-dgpay`<br>UAT: `uat-payby-dgpay` | - | - |
| password | - | Secret | SIM: `kv-biz-sim.payby-dgpay-http-password-01`<br>UAT: `kv-biz-uat.payby-dgpay-http-password-01`<br>PROD: `kv-biz-payby-prd.payby-dgpay-http-password-01` |

## 需提供给 DGPAY 的信息

向 DGPAY 交付以下凭证：

- PayBy 公钥的 **Modulus** 和 **Exponent**（来源见上文公私钥生成步骤）
- PayBy API Token 的 **username** 和 **password**

DgPay 联系人：`gokhan.leblebici@dgpays.com`

> 后续可参考 `ppc-运营-1-证书交换` 完成证书交换流程。
