---
title: PayBy 转账到银行 返回码总览
domain: payby-transfer-to-bank
kind: wiki_page
slug: payby-transfer-to-bank-return-codes
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:56e8e18c-82c1-4231-b586-2130e089c7da
tags: []
---

# PayBy 转账到银行 返回码总览

本页汇总 Transfer to Bank 相关 API 的通用返回码与业务返回码及处理建议。返回码统一通过 `ResponseHeader` 中的 `code` / `msg` 字段返回，配合 `applyStatus`（SUCCESS / FAIL / ERROR）判断申请状态。相关接口详见 [[payby-transfer-to-bank-overview]]，字段定义详见 [[payby-transfer-to-bank-data-models]]。

## 通用返回码（适用于所有 Transfer to Bank API）

以下返回码在 [[api_payby_transfer_get_iban_holder_name]]、[[api_payby_transfer_get_fundout_ability_list]]、[[api_payby_transfer_calculate_fundout]] 等接口中通用：

| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 0 | SUCCESS | 成功 | - |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API未授权 | 联系 PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API服务不可用 | 联系 PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系 PayBy，稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |

## 查询 IBAN 姓名 专属返回码

仅 [[api_payby_transfer_get_iban_holder_name]] 接口返回的业务码：

| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 62101 | WRONG_IBAN_FORMAT | 传入的 IBAN 格式不对 | 调整 iban |
| 62102 | NAME_NOT_FOUND | 无法通过 IBAN 查询姓名 | 调整 iban |
| 62103 | QUERY_API_UNAVAILABLE | 查询接口不可用 | 稍后重试 |

## applyStatus 与 code 的关系

- `applyStatus = SUCCESS`：申请成功，对应 `code = 0`。
- `applyStatus = FAIL`：申请失败，通常对应 4xx 业务类错误码（如 `INVALID_PARAMETER`、`UNAUTHORIZED`、`RISK_FAIL` 等）。
- `applyStatus = ERROR`：申请异常，通常对应 5xx 系统类错误码（如 `SYSTEM_ERROR`、`SERVICE_TIMEOUT`）。

## 处理建议分类

按错误类别给出统一的处置策略：

- **参数类（400）**：核对请求字段格式与必填项；检查 `requestTime` 是否在合理时间窗口内。
- **频控类（402）**：降低调用频率，必要时引入本地限流或退避重试。
- **授权/可用性类（403 / 404）**：检查商户授权状态与 API 路径，如确认无误请联系 PayBy。
- **系统类（500 / 504）**：可稍后重试；持续出现请联系 PayBy 排查。
- **风控类（601）**：根据业务场景核查交易合规性，调整业务后重试。
- **IBAN 业务类（621xx）**：仅出现在查询 IBAN 姓名接口，按 IBAN 格式校验、姓名匹配、接口可用性分别处理。
