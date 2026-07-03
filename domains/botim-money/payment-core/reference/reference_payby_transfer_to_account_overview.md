---
id: reference_payby_transfer_to_account_overview
object_type: Reference
name: PayBy转账到电子账户接口总览
aliases: [payby-transfer-to-account-overview]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
source_type: wiki
source_ref: api-docs/payby-transfer-v1.1-p1
tags: [payment-core, wiki-overview]
related_services: []
related_tables: []
---


# PayBy转账到电子账户接口总览

PayBy转账到电子账户（Transfer）面向企业商户提供把资金付款到PayBy个人账户或企业账户的能力，本页汇总该业务域的接入规则、通用字段和API清单。

## 阅读对象

面向商户系统（在线购物平台、人工/自动化收银系统等）接入PayBy的：
- 技术架构师
- 研发工程师
- 测试工程师
- 系统运维工程师

## 业务场景

- 企业付款到用户账户（个人或企业）。
- 通过商户订单号或PayBy订单号查询付款结果。
- PayBy在收款方到账后异步通知商户付款结果。

产品标识：`product = Transfer`（转账到PayBy账户的产品）。

## 接口协议规则

| 项目 | 说明 |
| --- | --- |
| 传输方式 | HTTPS |
| 提交方式 | POST |
| 数据格式 | JSON |
| 字符编码 | UTF-8 |
| 签名算法 | SHA256WithRSA |
| 签名要求 | 请求和响应都需要签名 |

请求参数中值为空则不予处理。

## 安全规则

### 签名

- 算法：SHA256WithRSA，私钥由商户自行颁发。
- 签名原文：请求 Http Body 的原始内容。
- 原文 UTF-8 编码，签名结果 Base64 编码。

私钥/公钥生成（openssl）：

```shell
# 生成密钥（≥2048）
openssl genrsa -out PayBy_key.pem 2048
# 导出公钥
openssl rsa -in PayBy_key.pem -out PayBy_key_public.pem -pubout
# 导出 Java 可用的 PKCS8 私钥
openssl pkcs8 -in PayBy_key.pem -topk8 -nocrypt -out PayBy_key_private.pem
```

### 加密

- 算法：RSA 公钥加密，公钥由 PayBy 颁发。
- 单字段加密原文一般不超过 200 字节。
- 明文 UTF-8 编码，密文 Base64 编码。
- 适用于敏感字段（如 `beneficiaryIdentity`、`beneficiaryFullName`）。

## 通用参数规定

### 货币类型 currency

| Currency | 说明 |
| --- | --- |
| AED | 阿联酋货币单位 |

### 商户订单号 merchantOrderNo

- 由商户自定义生成，仅支持字母、数字、中划线 `-`、下划线 `_` 的组合。
- 必须保持唯一（建议时间+随机序列）。
- 重发支付要使用原订单号，避免重复支付。
- 已支付或已取消的订单号不能重新发起。

### Http Header 通用字段

| 字段 | 必填 | 说明 |
| --- | --- | --- |
| Content-Language | Optional | 文案语言，如 `en` |
| Sign | Required | 签名 |
| Partner-Id | Required | 商户号 |

## 通用对象定义

### TransferOrder

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | |
| 商户订单号 | merchantOrderNo | Required | String(64) | |
| PayBy订单号 | orderNo | Required | String(32) | |
| 产品名称 | product | Required | String(200) | 例：Transfer |
| 订单状态 | status | Required | | CREATED/SUCCESS/FAILURE |
| 支付信息 | paymentInfo | Optional | TransferPaymentInfo | |
| 金额 | amount | Required | Money | |
| 收款方标识类型 | beneficiaryIdentityType | Required | String(200) | PHONE_NO / MEMBER_ID / TOTOK_UID |
| 收款人标识 | beneficiaryIdentity | Required | String(200) | PHONE_NO 时填带区号手机号；MEMBER_ID 时填 PayBy member ID；加密后传输；返回值为 sha256 后的值 |
| 收款方姓名 | beneficiaryFullName | Optional | String(200) | |
| 付款备注 | memo | Required | String(200) | |
| 后台通知地址 | notifyUrl | Optional | String(200) | |
| 错误代码 | failCode | Optional | String(50) | 见附录订单错误原因代码 |
| 错误描述 | failDes | Optional | String(200) | 订单失败原因 |

收款方选择规则：
- 商户使用 `MEMBER_ID`。
- 个人用户使用 `PHONE_NO`。

订单状态机：

| Status | 说明 |
| --- | --- |
| CREATED | 已创建 |
| SUCCESS | 已成功 |
| FAILURE | 已失败 |

### TransferPaymentInfo

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 付款人手续费 | payerFeeAmount | Optional | Money | |
| 预计到账时间 | arrivalTime | Optional | Timestamp(3) | PayBy 付款成功时间 |

### ResponseHeader

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求状态 | applyStatus | Required | String(16) | SUCCESS-申请成功 / FAIL-申请失败 / ERROR-申请异常 |
| 返回错误码 | code | Required | String(10) | 返回码 |
| 返回信息 | msg | Optional | String(200) | 返回信息 |

响应 Http Body 中的 `body` 字段仅当 `applyStatus = SUCCESS` 且 `code = 0` 时返回。

### OrderIndexRequest

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Optional | String(64) | 与 orderNo 二选一，不能同时为空也不能同时有值 |
| PayBy订单号 | orderNo | Optional | String(32) | |

## API 清单

| API | 说明 |
| --- | --- |
| [[api_transfer_place_transfer_order]] | 单笔付款到账户接口 `placeTransferOrder` |
| [[api_transfer_get_transfer_order]] | 查询单笔付款到账户订单接口 `getTransferOrder` |
| [[api_transfer_order_notify]] | 商户付款到账户成功通知 `transferOrder Notify` |

## 版本记录

| 版本 | 时间 | 修改点 |
| --- | --- | --- |
| v1.0 | 2021-10-12 | 初稿 |
| v1.1 | 2021-10-13 | 补充附录订单错误原因代码 |
