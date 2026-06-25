---
id: scn_online_business_openapi_protocol_signing
object_type: Scenario
name: 商户 Open API 接入协议与签名/加密规则
aliases: [open-api-protocol, 签名规则, SHA256WithRSA, 接口协议规则, 支付场景术语]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: api-docs/payby-api-v2.25 (protocol-rules / openapi-security-rules / payment-scenarios)
tags: [online-business, open-api, 签名, 加密, RSA, 商户接入, 支付场景]
related_services: [svc_sgs, svc_acquireii]
related_tables: []
related_logs: []
---

# 商户 Open API 接入协议与签名/加密规则

> 商户接入 PayBy 开放接口(Open API)调 API 时必须遵守的传输/签名/加密协议规则,以及支持的支付场景术语。来源:PayBy 开放接口文档 v2.25。QA 接入测试与签名联调的基准。

## 触发 / 入口
商户系统(在线购物平台 / 人工收银 / 自动化智能收银等)集成 PayBy,通过 [[svc_sgs]] 开放网关调用收单、退款、转账、对账、卡管理等接口。所有请求须满足以下协议与签名约定。

## 关联关系
- **涉及服务**:[[svc_sgs]](开放网关入口)、[[svc_acquireii]](收单)(= `related_services`)。
- **读写的表**:无(协议规则,不涉及业务表)。
- **相关接口**:对账单 [[api_payby_get_order_statement]];异步通知 [[scn_online_business_merchant_async_notify]]。

## 协议规则(传输 / 提交 / 编码)
| 方式 | 规则 |
| --- | --- |
| 传输方式 | HTTPS(保障交易安全) |
| 提交方式 | POST |
| 数据格式 | JSON |
| 字符编码 | UTF-8 |
| 签名算法 | SHA256WithRSA |
| 签名要求 | 请求和响应数据**双向**均需签名 |

公共请求约定:
- Http Header 必填:`Sign`、`Partner-Id`;可选 `Content-Language`(如 `en`)。
- Http Body 必填:`requestTime`(Timestamp(3))与 `bizContent`(业务内容)。

## 签名规则
- 算法:`SHA256WithRSA`。
- 私钥:由商户自己颁发并保管。
- 签名原文:请求 Http Body 的原始内容。
- 原文编码:UTF-8;签名结果编码:Base64。

## 加密规则
- 算法:`RSA` 公钥加密,公钥由 PayBy 颁发。
- 加密字段大小限制:一般不超过 200 字节。
- 规则:`RSA(加密原文)`;明文编码 UTF-8,密文编码 Base64。
- 敏感字段(如收款人 `holderName`/`iban`/`beneficiaryAddress`)加密传输、响应中以密文返回。

要点速查:
| 用途 | 算法 | 密钥来源 | 编码 |
| --- | --- | --- | --- |
| 签名 | SHA256WithRSA | 商户自有私钥 | UTF-8 原文 / Base64 签名 |
| 加密 | RSA | PayBy 颁发公钥 | UTF-8 明文 / Base64 密文 |

密钥生成(OpenSSL,至少 2048 位):
```shell
openssl genrsa -out PayBy_key.pem 2048                                      # 生成密钥
openssl rsa -in PayBy_key.pem -out PayBy_key_public.pem -pubout             # 导出公钥
openssl pkcs8 -in PayBy_key.pem -topk8 -nocrypt -out PayBy_key_private.pem  # 导出 Java 可用私钥(PKCS8)
```

## 支付场景术语(paySceneCode)
| 场景 | 说明 |
| --- | --- |
| JSAPI | 商户已有 H5 商城,用户在 PayBy 内访问该 H5 时调 PayBy 下单 |
| App 支付 | 移动端 APP 集成开放 SDK,拉起 PayBy 模块支付 |
| PAYPAGE(支付网页) | 浏览器跳转到 PayBy 支付网页完成支付 |
| 付款码支付 | 用户出示付款码,商户扫描后完成支付(线下面对面,见 [[scn_online_business_payment_code_scan]]) |
| 动态码支付 | 商户按协议生成二维码,用户用 PayBy"扫一扫";适用 PC 网站/实体店/广告/无人售卖机 |
| PAYANDSIGN(协议授权) | 提前签三方代扣协议取得授权令牌,后续用令牌直接扣款 |
| CASHTOPUP(现金充值) | 线上下单,用户到线下现金充值门店完成支付 |
| DIRECTPAY(直联) | 商户收集卡信息后经 API 直接发起支付;支持 DevicePay、分期(见 [[scn_online_business_direct_pay]]) |
| EWALLET(电子钱包) | 商户页面下单选定支付 APP 后返回移动应用拉起方式 |
| FACE | 刷脸支付 |

## DB 校验点
- 无(协议层规则)。

## 操作步骤 / 测试校验点(QA)
1. **协议校验**:非 HTTPS / 非 POST / 非 JSON / 非 UTF-8 请求应被拒。
2. **签名校验**:请求体改动一字节后签名应失败;响应签名须能用 PayBy 公钥验签通过。
3. **加密校验**:敏感字段未按 RSA 加密或超 200 字节应报错;密文须可被 PayBy 私钥解密。
4. **公共头/体**:缺 `Sign`/`Partner-Id`/`requestTime`/`bizContent` 应返回参数错误。
5. **支付场景**:各 paySceneCode 的下单参数集合(paySceneParams)与场景匹配(如 DIRECTPAY 的 installment、PAYANDSIGN 的 customerId)。

## 预期结果
- 合规请求(HTTPS+POST+JSON+UTF-8+正确签名+正确加密)被受理;任一项不合规被拒并返回对应错误。
