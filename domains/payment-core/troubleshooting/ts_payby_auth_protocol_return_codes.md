---
id: ts_payby_auth_protocol_return_codes
object_type: Troubleshooting
name: PayBy 授权协议签约 / 转账接口返回码排错
aliases:
- 授权协议返回码
- 签约返回码
- return codes
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: api-docs/payby-auth-agreement-v1.0.2-p2 + api-docs/payby-transfer-v1.1-p2
tags:
- 返回码
- error-code
- 签约协议
- 转账
related_services:
- svc_protocol
related_tables: []
related_logs: []
related_failures: []
---

# PayBy 授权协议签约 / 转账接口返回码排错

## 症状

对接 PayBy 授权协议签约（[[api_payby_apply_protocol]]、[[api_payby_get_protocol]]）或转账到电子账户接口时，响应体 `head.code` / `head.msg` 返回非 0 错误码，业务申请失败。需按返回码定位原因并修正。注意：业务是否成功还需结合 `head.applyStatus`（`SUCCESS`/`FAIL`/`ERROR`）综合判断。

## 关联关系

- **涉及服务**：[[svc_protocol]]（= `related_services`，暴露签约协议接口）
- **相关接口**：[[api_payby_apply_protocol]]、[[api_payby_get_protocol]]、[[api_payby_protocol_notify]]

## 可能根因（按码定位）

### 通用返回码（公共错误，适用所有签约 / 转账 API）

| code | msg | 原因 | 解决方案 |
| ---- | --- | ---- | -------- |
| 0    | SUCCESS               | 成功 | |
| 400  | INVALID_PARAMETER     | 参数错误 | 调整请求参数 |
| 400  | REQUESTTIME_TOO_EARLY | 请求时间比当前早太多 | 调整请求时间 |
| 400  | REQUESTTIME_TOO_LATER | 请求时间比当前晚太多 | 调整请求时间 |
| 402  | RATE_LIMIT_REJECT     | 请求过于频繁 | 降低请求频率 |
| 403  | UNAUTHORIZED          | API 未授权 | 联系 PayBy |
| 404  | SERVICE_NOT_AVAILABLE | API 服务不可用 | 联系 PayBy |
| 500  | SYSTEM_ERROR          | 系统错误 | 联系 PayBy，稍后重试 |
| 504  | SERVICE_TIMEOUT       | 服务超时 | 稍后重试 |
| 601  | RISK_FAIL             | 风控校验失败 | 请调整业务 |

### 申请签约协议专属（applyProtocol，`/sgs/api/protocol/applyProtocol`）

| code | msg | 原因 | 解决方案 |
| ----- | --- | ---- | -------- |
| 90001 | MISSING_IAP_DEVICE_ID             | 缺少 deviceId | 调整请求参数 |
| 90002 | MISSING_APP_ID                    | 缺少 appId | 调整请求参数 |
| 90003 | INVALID_APP_ID                    | 无效的 appId | 调整请求参数 |
| 90004 | INVALID_LANG_TYPE                 | 无效的语言类型 | 调整请求参数 |
| 90006 | INVALID_PROTOCOL_SCENE_CODE       | 无效的 protocolSceneCode | 调整场景代码 |
| 90007 | EXPIREDTIME_ILLEGAL               | 过期时间非法 | 调整过期时间 |
| 90008 | EXPIREDTIME_LESS_THAN_REQUESTTIME | 过期时间小于请求时间 | 调整过期时间 |
| 90009 | INVALID_ACCESS_TYPE               | 无效的 accessType | 调整请求参数 |

- `90001`/`90002` 通常出现在 `accessType=SDK` 下未填 `protocolSceneParams.iapDeviceId` 或 `appId`。
- `90009` 为 v1.0.1 新增，校验 `accessType` 必须为 `SDK` 或 `H5`。

### 查询协议专属（getProtocol，`/sgs/api/protocol/getProtocol`）

| code | msg | 原因 | 解决方案 |
| ----- | --- | ---- | -------- |
| 90005 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |

### 转账到电子账户接口专属（订单 / 业务关系类）

| code | msg | 原因 | 解决方案 |
| ----- | --- | ---- | -------- |
| 62002 | ORDER_FAILURE               | 已失败订单再次发起撤销 / 退款 | 调整商户订单号 |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |
| 62016 | MERCHANT_ORDER_NO_EXIST     | 订单号相同但业务参数不同的创建请求 | 调整订单号 |
| 62020 | PAYERMID_PAYEEMID_ARE_SAME  | 付款人和收款人相同 | 调整付款人/收款人 |
| 62023 | NAME_NOT_MATCH              | 收款人姓名不符 | 调整收款人姓名 |
| 62026 | PRODUCT_IS_NOT_APPLIED      | 产品未申请 | 请申请产品 |
| 62027 | BENEFICIARY_NOT_EXIST       | 收款人不存在 | 调整收款人 |
| 62028 | ORDER_SUCCESS               | 订单已成功 | 调整商户订单号 |
| 62029 | ORDER_CREATED               | 订单已创建 | 调整商户订单号 |

### 转账订单错误原因代码（风控 / 限额 / 渠道细分）

| code | msg | 原因 | 解决方案 |
| ----- | -------------------------------------------- | ---------------- | ------------ |
| 92000 | Risk control rejection                       | 风控拒绝 | 请调整业务 |
| 92001 | The amount of transaction exceeds the limit  | 交易金额超限 | 请调整业务 |
| 92002 | The number of transactions exceeds the limit | 交易次数超限 | 请调整业务 |
| 92003 | Non KYC user transactions                    | 用户未完成 KYC | 请调整业务 |
| 92004 | Channel rejection                            | 渠道拒绝 | 请调整业务 |

## 排查步骤 / 处理

- **`400` 系列**：先核对请求体字段、字段类型与 `requestTime`（毫秒级时间戳，与服务器时间偏差不能过大）。
- **`402` / `504`**：客户端加退避重试。
- **`403` / `404`**：通常与商户号未授权或环境（联调/生产）URL 错误有关，确认 `Partner-Id` 与签名 `Sign` 是否匹配该环境的密钥对。
- **`500`**：建议保留 `traceCode` 后联系 PayBy。
- **`601` / `92000`～`92004`**：触发风控，按子码调整业务（金额、频次、KYC 状态、渠道选择等）后重试。
- **`62xxx` 订单状态类**：均与商户订单号语义冲突有关，调整商户订单号后重试。
- **`90xxx` 段**：均为签约业务参数校验类错误，按 `msg` 提示修正对应字段即可。
