---
title: PPC交易账务API清单
domain: ppc-card-business
kind: wiki_page
slug: ppc-api-transaction
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2133098640
tags: []
---

# PPC交易账务API清单

本页汇总 PPC 系统中与交易明细、充值、外币兑换、对账下载相关的 API。其它接口分类参见 [[ppc-api-inventory-overview]]、[[ppc-api-card-management]]、[[ppc-api-card-network-inbound]]。

> Path 为推断格式，待后端确认。实时接口文档见 [[ppc-api-gateways]] 中的 Smart-doc 地址。

## 接口清单

| 操作 | Method | Path（推断） | 调用方 | 备注 |
|---|---|---|---|---|
| 查询交易明细 / Get transactions | GET | `/ppc/card/v1/transactions` | App | — |
| 充值 / Top-up (add funds) | POST | `/ppc/card/v1/add-funds` | App | — |
| 货币转换 / Currency convert | POST | `/ppc/fx/v1/convert` | App | — |
| 汇率试算 / FX calculate | POST | `/ppc/fx/v1/calculate` | App | 弱网键盘关闭后不应调用（BUG-6529） |
| 下载交易单 / Download statement | GET | `/ppc/card/v1/statement` | App / H5 | — |

调用方均经由 CGS 网关接入，详见 [[ppc-api-gateways]]。

## 关联的账务事件来源

交易/账务数据由卡组织入向回调驱动，本页不展开，详见 [[ppc-api-card-network-inbound]]：

- `Authorization` 回调 → 写入授权流水、设置 Pending Account
- `Clearing / Settle` 回调 → Pending → Settle / Refund / Reversal

交易类型枚举 `T/S/R/RL/F/CB/RF/FRL` 定义见外部参考 `ppc-OP-3-Fee Config`；账务细节见 `ppc-SD-3-Transaction`。

## 错误码与异常场景

通用错误码（完整表见 [[ppc-api-error-codes]]）中，本页 API 高相关项：

- `PROCESSING_EXCEPTION` — 上下游（YSE/trade/grc）异常，需测试重试机制
- `SYSTEM_EXCEPTION` — 兜底，必测降级
- `IDENTITY_VERIFY_FAILED` — 敏感查询/下载前置核身失败

## 测试用例生成要点

详见 [[ppc-api-test-case-generation-hints]]，本页 API 应特别覆盖：

- **字段边界**：金额（精度 / 边界 / 负数）、币种（合法 / 非法 ISO）。
- **FX 试算**：`/ppc/fx/v1/calculate` 在弱网/键盘关闭场景下不应被触发（回归 BUG-6529）。
- **充值幂等**：`add-funds` 重复请求需返回相同结果且 DB 不创建新记录。
- **对账单下载**：H5 与 App 双入口、大数据量分页/超时、失效 `identity_verify_token` 必拒。
- **回调时序**：Authorization / Clearing 乱序、重投、丢失、超时 → 验证幂等 + 兜底对账，影响交易明细一致性。

## 参考

- `ppc-SD-3-Transaction` — Authorization / Clearing / Reversal 账务细节
- `ppc-OP-3-Fee Config` — 交易类型枚举
- `ppc-2-流程图设计` — 服务交互图
- API 文档实时入口：`https://sim-admin.corp.test2pay.com/api-doc/`
