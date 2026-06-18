---
title: PayBy 转账到银行账户接口总览
domain: payby-transfer-to-bank
kind: wiki_page
slug: payby-transfer-to-bank-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:56e8e18c-82c1-4231-b586-2130e089c7da
tags: []
---

# PayBy 转账到银行账户接口总览

本页汇总 PayBy「转账到银行账户（Transfer to Bank）」产品对接的总体规则，包括读者对象、版本演进、协议与参数规范、签名与加密安全规则、API 清单。具体字段定义见 [[payby-transfer-to-bank-data-models]]，错误码集中说明见 [[payby-transfer-to-bank-return-codes]]。

## 阅读对象

面向商户系统（在线购物平台、人工收银系统、自动化智能收银系统等）集成 PayBy 时涉及的：

- 技术架构师
- 研发工程师
- 测试工程师
- 系统运维工程师

## 版本演进

| 版本 | 时间 | 修改点 |
| --- | --- | --- |
| v2.0.0 | 2021-10-12 | 初稿 |
| v2.0.1 | 2021-12-02 | 新增 bankReference |
| v2.1 | 2022-03-01 | 增加国际汇款通道；增加出款能力查询接口；增加试算接口 |
| v2.2 | 2024-08-20 | 增加 IBAN 查询姓名接口 |

## 术语

- **PayBy 支付系统**：完成 PayBy 支付流程中涉及的 API 接口、后台业务处理系统、回调通知等系统的总称。

## 协议规则

商户接入 PayBy 支付系统调用 API 必须遵守以下规则：

| 方式 | 说明 |
| --- | --- |
| 传输方式 | HTTPS |
| 提交方式 | POST |
| 数据格式 | JSON |
| 字符编码 | UTF-8 |
| 签名算法 | SHA256WithRSA |
| 签名要求 | 请求和响应数据都需要签名 |

## 参数规范

### 请求参数处理

- 如果请求参数的值为空，则不予处理。

### 货币类型（currency）

| Currency | 说明 |
| --- | --- |
| AED | 阿联酋货币单位 |

### 商户订单号（merchantOrderNo）

- 由商户自定义生成。
- 仅支持字母、数字、中划线 `-`、下划线 `_` 的英文半角组合。
- 必须保持唯一性（建议使用「当前系统时间 + 随机序列」生成）。
- 重新发起一笔支付应复用原订单号，避免重复支付。
- 已支付过或已调用取消交易的订单号不能重新发起支付。

### 产品（product）

| 产品名称 | 产品说明 |
| --- | --- |
| Transfer to bank | 转账到银行卡的产品 |

> 完整字段类型定义（TransferToBankOrder、TransferToBankPaymentInfo、ResponseHeader、OrderIndexRequest、IbanHolderName 等）见 [[payby-transfer-to-bank-data-models]]。

## 安全规则

### 签名算法

1. 使用 **SHA256WithRSA** 算法签名，私钥由商户自己颁发。
2. 签名原文规则：请求 Http Body 原始内容。
3. 原文使用 UTF-8 编码。
4. 签名结果使用 Base64 编码。

私钥产生建议操作：

```shell
### 生成密钥（至少 2048 位）
openssl genrsa -out PayBy_key.pem 2048

### 导出公钥
openssl rsa -in PayBy_key.pem -out PayBy_key_public.pem -pubout

### 导出 Java 可用的私钥
openssl pkcs8 -in PayBy_key.pem -topk8 -nocrypt -out PayBy_key_private.pem
```

### 加密算法

1. 使用 **RSA** 公钥加密，公钥由 PayBy 颁发。
2. 加密字段不宜过大，一般不超过 200 字节。
3. 加密规则：`RSA(加密原文)`。
4. 明文使用 UTF-8 编码。
5. 加密结果使用 Base64 编码。

### 通用 Http Header

所有接口请求/响应都需携带：

| 字段名 | 变量名 | 必填 | 说明 |
| --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | 例 en（英文） |
| 签名 | Sign / sign | Required | 签名值 |
| 商户号 | Partner-Id | Required | 商户号（12 位） |

## API 清单

转账到银行产品当前对外提供以下接口：

| 接口 | 用途 | 起始版本 |
| --- | --- | --- |
| [[api_payby_transfer_get_iban_holder_name]] | 校验用户名称与 IBAN 账号是否匹配 | v2.2 |
| [[api_payby_transfer_get_fundout_ability_list]] | 查询商户可出款的国家/币种/网络能力 | v2.1 |
| [[api_payby_transfer_calculate_fundout]] | 出款试算（汇率与手续费） | v2.1 |

各接口的请求/响应详情见对应子页；公共返回码与业务返回码集中见 [[payby-transfer-to-bank-return-codes]]。
