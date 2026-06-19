---
title: 商户收单测试数据准备规范
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-test-data-conventions
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:4ef3640b-38b5-4756-81d5-d729c241dc79
tags: []
---

# 商户收单测试数据准备规范

本页定义商户收单测试中通用的测试数据约定：订单号命名、金额选择、测试卡号、特殊 expiry 触发、notifyUrl mock 工具。所有场景手册的用例数据都应遵循本页规范。相关方法论参见 [[merchant-acquisition-test-methodology-overview]]，环境与账号信息见 [[merchant-acquisition-test-environment-and-tools]]。

## merchantOrderNo 命名

强烈建议固定格式：

```
QA_<场景>_<时间戳>_<可选标记>
```

示例：

- `QA_PREAUTH_1714478400_3892`
- `QA_PAYPAGE_DCC_ACCEPT_1714478500`
- `QA_REFUND_PARTIAL_1714478600`

理由：

- `QA_` 前缀方便后续清洗测试数据
- 场景标识方便排查时一眼识别
- 时间戳保证唯一性，避开 `62016 MERCHANT_ORDER_NO_EXIST` 幂等冲突
- 可选标记区分子场景（如 `DCC_ACCEPT`、`PARTIAL`）

## 金额选择

按用例目的挑选金额，避免随手写数字：

| 金额段 | 用途 | 备注 |
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

## 测试卡号速查

| 卡号 | 品牌 | 国家/地区 | 用途 |
|---|---|---|---|
| `5123 4500 0000 0008` | MasterCard | AE | Local MC 标准测试 |
| `2223 0000 0000 0007` | MasterCard | JP | International MC（5111 不支持 3DS 时改用） |
| `5111 1111 1111 1118` | MasterCard | JP | International MC（部分场景） |
| `4012 0000 3333 0026` | Visa | GB→AE | Local Visa |
| `4508 7500 1574 1019` | Visa | AE→GB | International Visa |
| `4273 1490 1979 9094` | Visa | — | DCC 外币卡 |
| `4242 4242 4242 4242` | Visa | — | 通用测试卡 |

有效期通用值：`01/39`（永久有效，避免年到期问题）。

## 特殊 expiry 模拟（仅 MPGS 模拟环境）

通过给测试卡填入特定 expiry，触发渠道返回不同结果，用于覆盖 B 组异常用例：

| Expiry | 渠道返回 |
|---|---|
| `01/39` | APPROVED |
| `05/39` | DECLINED |
| `04/27` | EXPIRED_CARD |
| `08/28` | TIMED_OUT |
| `01/37` | ACQUIRER_SYSTEM_ERROR |
| `02/37` | UNSPECIFIED_FAILURE |
| `05/37` | UNKNOWN |

错误码与异常 case 的对应关系参见 [[merchant-acquisition-error-code-quickref]]。

## 模拟回调 / notifyUrl

推荐工具：

- **webhook.site** —— 一次性接收回调，直接看 body
- **ngrok / frp** —— 暴露本地 mock 服务
- 公司内部回调测试服务（如有）

测试要点：

- 验证通知 body 字段完整
- 故意返回非 `SUCCESS` / 非 200 / 超时 → 验证重试时间表（`2 → 10 → 10 → 60 → 120 → 360 → 900` 分钟）
- 验证 7 次后停止重试

通知重试详细策略与对账单结构见 [[merchant-acquisition-notify-and-statement]]；如何把 notifyUrl 串到 curl 请求里见 [[merchant-acquisition-curl-postman-skeleton]]；每笔交易完整核对项见 [[merchant-acquisition-per-transaction-checklist]]。
