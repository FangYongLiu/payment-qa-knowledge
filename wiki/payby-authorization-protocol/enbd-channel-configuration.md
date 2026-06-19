---
title: ENBD渠道配置说明
domain: authorization-protocol
kind: wiki_page
slug: enbd-channel-configuration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:80ee74c1-158f-4e61-910f-b28260880f1a
tags: []
---

# ENBD渠道配置说明

本页说明 ENBD（Emirates NBD）渠道在 `payby-authorization-protocol` 域下的 YAML 配置项，重点关注证书、token、受益人校验接口及 `remark` 动态字段配置。

## 顶层结构

配置根节点为 `enbd`，主要包含 `iban` 与 `channel` 两块。

- `iban.mock: true`：IBAN 走 mock 模式。
- `channel`：渠道集成设置，下含 `chargeSha`、`certificate`、`token`、`beneficiaryValidation`、`config`、`remark` 等子项。

## chargeSha

- `merchantList: 200000030907`：参与 chargeSha 的商户列表。

## 证书配置（certificate）

- `filePath: kv-biz-sim.3rdenbd-api-certificate-01`
- `password: kv-biz-sim.3rdenbd-api-certpassword-01`

## Token 接口（token）

- `url: https://authuat.emiratesnbd.com/token`

## 受益人校验（beneficiaryValidation）

- `url: https://openapiuat.emiratesnbd.com/open-banking/payment/v1/beneficiary/account/`

## 渠道参数（config）

| 字段 | 值 |
|---|---|
| `financialId` | `EBI` |
| `channelId` | `OBP` |
| `clientSecret` | `kv-biz-sim.3rdenbd-api-clientsecret-01` |
| `clientId` | `786140fa` |
| `encryptedKey` | `kv-biz-sim.3rdenbd-api-encryptedkey-01` |
| `signatureKey` | `kv-biz-sim.3rdenbd-api-signaturekey-01` |

## remark 动态字段（重点）

`remark` 节点用于控制汇款备注信息的生成规则，是文档重点关注项。

### useMerchantName

- 取值：`200013101398,200000428736,200000030907`
- 含义：上述商户在 remark 中使用商户名称。

### merchantDynamic

- 用于按匹配条件动态替换 remark 内容。
- 示例片段（原文截断）：
  ```yaml
  merchantDynamic: '[{"match":{"beneficiaryIban":"AE370260001011116428114"},"replace":true,"front":false,"fixed...
  ```
- 关键属性：
  - `match`：匹配条件，例如按 `beneficiaryIban` 命中指定收款 IBAN。
  - `replace`：是否进行替换。
  - `front`：是否拼接在前。
  - `fixed`：固定文案（原文截断，未完整展示）。
