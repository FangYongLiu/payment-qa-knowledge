---
title: PayBy授权协议签约总览
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-auth-protocol-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:21faec0e-f55f-4035-a6ea-c17499da3582
tags: []
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

## 接入前置：商户入驻

接入授权协议签约前，商户需先在 **PayBy Merchant Portal（商户控台）** 完成入驻。入驻为多步骤表单流程，主要包含以下步骤：

1. **Company Profile**（公司资料）
2. **Company Credentials**（公司资质）
3. **Management**（管理人员）

### Company Profile 关键字段

公司资料部分包含以下信息（标 * 为必填）：

- **Company name\***：公司名称，需与营业执照（trade license）一致
- **Company website**：公司官网
- **Industry\***：所属行业（下拉选择）
- **High-Risk Jurisdiction Involvement\***：是否涉及高风险司法辖区
- **Monthly Turnover\***：月营业额
- **Payment Method Accepted\***：受理支付方式

### Registered Address（注册地址）

地址需与营业执照登记一致：

- **Company number\***：联系电话（含国家区号，如 `+971`）
- **Email address\***：邮箱
- **Country\***：国家（默认 United Arab Emirates）
- **Emirates\***：所在酋长国/城市
- **Area\***：区域
- **Building Name\***：楼宇名称
- **Office No.\***：办公室号
- **Are registered address and company address the same?\***：注册地址与办公地址是否一致（yes/no）

### Tax Certificate（税务）

- **Is the company VAT-registered?\***：是否已注册 VAT（yes/no）

操作上提供 **Save Draft**（保存草稿）与 **Continue**（继续下一步）两个按钮。

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
| 协议状态 | protocolStatus | Optional | String(32) | EXPIRED-已过期
