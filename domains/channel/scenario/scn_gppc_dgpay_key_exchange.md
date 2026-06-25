---
id: scn_gppc_dgpay_key_exchange
object_type: Scenario
name: GPPC-DGPAY 渠道密钥交换与配置
aliases: [DGPAY密钥交换, GPPC DGPay key exchange]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/1142947906
tags: [gppc, dgpay, key-exchange, rsa, key-vault, 渠道配置]
related_services: []
related_tables: []
related_logs: []
---

# GPPC-DGPAY 渠道密钥交换与配置

## 触发 / 入口
PayBy 与 DGPAY 对接时所需的 RSA 公私钥生成、API Token 配置,以及双方需互相提供的凭证与 Key Vault 存储路径。用于渠道接入/联调前的密钥准备与配置核对。
注:GPPC / DGPAY 服务对象域内尚未建,待补。

## 关联关系
- **涉及服务**:GPPC、DGPAY 渠道(对象待补)
- **DgPay 联系人**:`gokhan.leblebici@dgpays.com`

## 前置条件 / 交换凭证总览
- PayBy 提供给 DGPAY:Public Key 的 `Modulus` 与 `Exponent`;API Token 的 `username` 与 `password`。
- DGPAY 提供给 PayBy:Token `username`(`ASTRATECH`)与 `password`;Public Key 的 `Modulus` 与 `Exponent`。

## 操作步骤
### 生成 PayBy 私钥/公钥(1408 位 RSA,pkcs8)
```bash
openssl genrsa -out private.pem 1408
openssl rsa -in private.pem -pubout -out public.pem
openssl rsa -in private.pem -check
openssl pkcs8 -in private.pem -topk8 -nocrypt -out private_pkcs8.pem
openssl rsa -pubin -in public.pem -text -noout -modulus
```
把 public key 的 `Modulus` 与 `Exponent` 提供给 DGPAY。

### PayBy 公私钥 Key Vault 存储
| subject | Vault Type | Vault Key(SIM / UAT / PROD) |
|---|---|---|
| PayBy Public Key | Certificate | `kv-biz-sim.payby-dgpay-rsa-publickey-01` / `kv-biz-uat.payby-dgpay-rsa-publickey-01` / `kv-biz-payby-prd.payby-dgpay-rsa-publickey-01` |
| PayBy Private Key | Secret | `kv-biz-sim.payby-dgpay-rsa-privatekey-01` / `kv-biz-uat.payby-dgpay-rsa-privatekey-01` / `kv-biz-payby-prd.payby-dgpay-rsa-privatekey-01` |

### DGPAY 集成配置
| subject | key | value | Vault Key(SIM/UAT/PROD) |
|---|---|---|---|
| DGPAY TOKEN | username | `ASTRATECH` | - |
| DGPAY TOKEN | password | dgpay 提供 | `kv-biz-sim.3rddgpay-http-password-01` / `kv-biz-uat...` / `kv-biz-3rddgpay-prd...` |
| Public Key | Modulus | dgpay 提供 | `kv-biz-sim.3rddgpay-publickey-modulus-01` / uat / prd |
| Public Key | Exponent | dgpay 提供 | `kv-biz-sim.3rddgpay-publickey-exponent-01` / uat / prd |

### 生成 PayBy API Token
| subject | key | value | Vault Key |
|---|---|---|---|
| PAYBY TOKEN | username | SIM `sim-payby-dgpay` / UAT `uat-payby-dgpay` | - |
| PAYBY TOKEN | password | - | `kv-biz-sim.payby-dgpay-http-password-01` / uat / prd |

## DB / 校验点
- 各环境(SIM/UAT/PROD)Key Vault 的 publickey/privatekey/password/modulus/exponent 是否正确注入。

## 预期结果
- 双方公钥 Modulus/Exponent 与 Token username/password 已正确交换并入 Key Vault,联调可走加密链路。
> TODO:参考 `ppc-运营-1-证书交换`。
