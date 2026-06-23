---
title: 测试数据准备规范
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-test-data-preparation
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2125922317
tags: []
---

# 测试数据准备规范

本页约定商户收单测试中**测试数据的产出规范**：订单号命名、金额取值、测试卡号清单、模拟回调工具的使用方式。遵循这些规范可让用例可追溯、可清洗、可复用，并能精准触发各类边界与渠道返回。

## merchantOrderNo 命名

固定格式：

```
QA_<场景>_<时间戳>_<可选标记>
```

示例：

- `QA_PREAUTH_1714478400_3892`
- `QA_PAYPAGE_DCC_ACCEPT_1714478500`
- `QA_REFUND_PARTIAL_1714478600`

约定理由：

- `QA_` 前缀：方便后续清洗测试数据
- 场景标识：排查时一眼识别用途
- 时间戳：保证唯一性，避开 `62016 MERCHANT_ORDER_NO_EXIST` 幂等冲突
- 可选标记：区分子场景（如 `DCC_ACCEPT`、`PARTIAL`、`3DS` 等）

## 金额选择

按用途选取金额，覆盖正向、边界与风控：

| 金额 | 用途 | 备注 |
|---|---|---|
| `0` | 测错误码 | `400 invalid parameter: totalAmount` |
| `0.01` | 最小有效金额 | 测精度边界 |
| `1` / `10` | 普通用例 | 不触发密码 |
| `< 100` | MOTO 场景 | MPGS 渠道码会变 |
| `= 100` | 标准用例 | — |
| `499.99` | 不触发密码边界 | — |
| `500` | 触发密码验证边界 | ≥500 必须输密码 |
| `1,000,000` | 触发风控限额 | 必拒 |
| `9,999,999.99` | `decimal(12,2)` 上限 | 测格式 |

配合错误码与风控用例选择，详见 [[merchant-acquisition-error-code-cheatsheet]]。

## 测试卡号速查

UAT 默认通用卡（来自官方）：

- Card Number: `5123 4500 0000 0008`
- Expiry: `05/31`
- CVV2: `100`

按品牌 / 地域选卡：

| 卡号 | 品牌 | 国家/地区 | 用途 |
|---|---|---|---|
| `5123 4500 0000 0008` | MasterCard | AE | Local MC 标准测试 |
| `2223 0000 0000 0007` | MasterCard | JP | International MC（5111 不支持 3DS 时改用） |
| `5111 1111 1111 1118` | MasterCard | JP | International MC（部分场景） |
| `4012 0000 3333 0026` | Visa | GB→AE | Local Visa |
| `4508 7500 1574 1019` | Visa | AE→GB | International Visa |
| `4273 1490 1979 9094` | Visa | — | DCC 外币卡 |
| `4242 4242 4242 4242` | Visa | — | 通用测试卡 |

### 有效期通用值

- `01/39`：永久有效，避免年到期问题

### 用 expiry 触发渠道返回（仅 MPGS 模拟环境）

| Expiry | 渠道返回 |
|---|---|
| `01/39` | APPROVED |
| `05/39` | DECLINED |
| `04/27` | EXPIRED_CARD |
| `08/28` | TIMED_OUT |
| `01/37` | ACQUIRER_SYSTEM_ERROR |
| `02/37` | UNSPECIFIED_FAILURE |
| `05/37` | UNKNOWN |

主要用于 [[merchant-acquisition-test-case-skeleton-abcde]] 中 B 组（异常流程）的渠道侧错误模拟。

## 模拟回调 / notifyUrl

### 推荐工具

- **webhook.site**：一次性接收回调，直接看请求 body
- **ngrok / frp**：暴露本地 mock 服务到公网
- 公司内的回调测试服务（如有）

### 测试要点

- 验证 body 字段完整（订单对象、`notify_id`、`notify_timestamp` 等）
- 故意返回非 `SUCCESS` / 非 200 / 超时 → 验证重试时间表：`2 → 10 → 10 → 60 → 120 → 360 → 900`（分钟）
- 验证 7 次后停止重试

异步通知的完整重试策略与对账文件结构见 [[merchant-acquisition-notify-statement-spec]]；调用骨架见 [[merchant-acquisition-curl-postman-templates]]；每笔交易的端到端核对见 [[merchant-acquisition-per-transaction-checklist]]。
