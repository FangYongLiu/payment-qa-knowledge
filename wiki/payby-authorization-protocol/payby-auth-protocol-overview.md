---
title: PayBy授权协议签约总览
domain: authorization-protocol
kind: wiki_page
slug: payby-auth-protocol-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-auth-agreement-v1.0.2-p1
tags: []
related_services:
  - svc_authorization_service
  - svc_authorization_token
---

# PayBy授权协议签约总览

本页介绍 PayBy 授权协议签约的接入规则、协议场景配置以及通用字段类型定义，作为对接 PayBy 三方签约（商户会员 & 商户 & PayBy）业务的入口说明。

## 业务场景

授权协议签约用于发起 **商户会员 & 商户 & PayBy** 的三方签约，为后续基于协议的扣款（如付款授权场景）提供前置授权关系。

围绕协议签约，PayBy 提供以下接口能力：

- [[api_payby_apply_protocol]]：申请签约协议
- [[api_payby_get_protocol]]：查询协议状态/协议号
- [[api_payby_protocol_notify]]：协议状态变更后台异步通知

返回码统一汇总见 [[payby-auth-protocol-return-codes]]。

## 接口规则

### 协议规则

| 方式 | 说明 |
| --- | --- |
| 传输方式 | HTTPS |
| 提交方式 | POST |
| 数据格式 | JSON |
| 字符编码 | UTF-8 |
| 签名算法 | SHA256WithRSA |
| 签名要求 | 请求和响应数据都需要签名 |

### 参数规定

- 请求参数的值为空时，不予处理。
- 商户订单号 `merchantOrderNo` 由商户自定义生成，仅支持字母、数字、`-`、`_` 的英文半角组合。
- `merchantOrderNo` 必须保持唯一（建议使用当前系统时间 + 随机序列）。
- 重新发起同一笔支付应使用原订单号，避免重复支付；已支付或已取消的订单号不能重新发起支付。

### 协议场景代码（protocolSceneCode）

| protocolSceneCode | 说明 |
| --- | --- |
| 110 | 付款授权 |

### 协议场景参数关系

`accessType` & `protocolSceneCode` & `protocolSceneParams` & `interActionParams` 关系如下：

| accessType | protocolSceneCode | protocolSceneParams | interActionParams |
| --- | --- | --- | --- |
| SDK | 110 | iapDeviceId（必填）、appId（必填） | tokenUrl |
| H5 | 110 | redirectUrl（可空） | tokenUrl |

`tokenUrl`：包含 Token 的 URL 链接，商户系统可使用 token 或完整 URL 拉起 PayBy 完成支付。**有效期为 1 小时**，超期请使用相同业务内容参数重新发起以获取新的 tokenUrl。

### 安全规则

#### 签名

1. 算法：SHA256WithRSA，私钥由商户自行颁发。
2. 签名原文：请求 Http Body 原始内容。
3. 原文使用 UTF-8 编码。
4. 签名结果使用 Base64 编码。

私钥生成示例：

```shell
# 生成密钥（至少 2048 位）
openssl genrsa -out PayBy_key.pem 2048

# 导出公钥
openssl rsa -in PayBy_key.pem -out PayBy_key_public.pem -pubout

# 导出 Java 可用的私钥
openssl pkcs8 -in PayBy_key.pem -topk8 -nocrypt -out PayBy_key_private.pem
```

#### 加密

1. 算法：RSA 公钥加密，公钥由 PayBy 颁发。
2. 加密字段不宜过大，一般不能超过 200 字节。
3. 规则：`RSA(加密原文)`。
4. 明文使用 UTF-8 编码。
5. 加密结果使用 Base64 编码。

## 通用字段类型说明

### interActionParams

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 令牌地址 | tokenUrl | Required | String(200) | URL 地址 |

### ResponseHeader

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求状态 | applyStatus | Required | String(16) | SUCCESS-申请成功；FAIL-申请失败；ERROR-申请异常 |
| 返回错误码 | code | Required | String(10) | 返回码 |
| 返回信息 | msg | Optional | String(200) | 返回信息 |

### OrderIndexRequest

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Optional | String(64) | 与 orderNo 二选一，不能同时为空，且不能同时有值 |
| PayBy订单号 | orderNo | Optional | String(32) | — |

### Protocol

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Required | String(64) | — |
| PayBy协议号 | authProtocolNo | Optional | String(32) | — |
| 申请签约状态 | applySignStatus | Required | String(32) | APPLYING-申请中；CLOSED-关闭（未签署）；SIGNED-已签署；FAILURE-签署失败 |
| 签约时间 | signTime | Optional | Timestamp(3) | — |
| 生效时间 | effectTime | Optional | Timestamp(3) | — |
| 失效时间 | invalidTime | Optional | Timestamp(3) | — |
| 协议状态 | protocolStatus | Optional | String(32) | EXPIRED-已过期；TERMINATED-已解约；EFFECTIVE-有效；INEFFECTIVE-无效 |
| 签约人ID | signerId | Optional | String(32) | 签约人在 PayBy 的会员 ID |
| 扣除类型 | deductType | Optional | String(32) | SP = Single Pay Method |
| 扩展信息 | extension | Optional | Map<String,String> | 详见下文 |

#### extension 扩展信息

- `payMethodType`：用户选择的支付方式，取值 `BALANCE`、`CARD_PAY`
- `lastFour`：银行卡后 4 位
- `cardBrand`：卡组织

| code | description |
| --- | --- |
| VISA | VISA |
| MASTERCARD | MASTERCARD |
| CUP | CHINA UNION PAY |
| JCB | JCB |
| DINERS | DINERS CLUB INTERNATIONAL |
| MAESTRO | MAESTRO |
| AE | AMERICAN EXPRESS |
| EBT | EBT |
| DISCOVER | DISCOVER |
| CIRRUS | CIRRUS |
| RUPAY | RUPAY |
| UATP | UATP |
| ELO | ELO |

## 版本说明

| 版本 | 时间 | 修改点 |
| --- | --- | --- |
| v1.0.0 | 2020-08-14 | 初稿 |
| v1.0.1 | 2021-10-08 | 申请签约协议新增请求参数 `accessType`；调整协议场景参数关系；申请签约协议新增返回码 90009 |
| v1.0
