---
title: PPC卡管理API清单
domain: ppc-card-business
kind: wiki_page
slug: ppc-api-card-management
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2133098640
tags: []
---

# PPC卡管理API清单

本页汇总 PPC 卡生命周期相关 API（虚拟卡/实体卡申请、PIN、锁卡/解锁、替换、关闭、激活、配送跟踪），含调用方、关键字段与幂等键。Path 为推断格式，待后端确认。交易/账务、卡组织回调、错误码请见交叉链接。

## 调用方与网关

- App 侧通过 [[ppc-api-gateways]] 中的 CGS（`gp024_cgs`）接入。
- 实时接口文档：`https://sim-admin.corp.test2pay.com/api-doc/`
- 总览见 [[ppc-api-inventory-overview]]。

## 卡概览与申请

| 操作 | Method | Path（推断） | 关键字段 | 幂等键 |
|---|---|---|---|---|
| 获取卡概览 | GET | `/ppc/card/v1/summary` | `member_id` | — |
| 申请虚拟卡 | POST | `/ppc/card/v1/apply-virtual` | `member_id`, `card_type`(MC/PR), `kyc_token` | `member_id + card_type + session_id` |

- 申请前置：KYC 通过，否则返回 `KYC_NOT_VERIFIED`。

## PIN 管理

| 操作 | Method | Path（推断） | 关键字段 | 备注 |
|---|---|---|---|---|
| 设置 PIN | POST | `/ppc/card/v1/set-pin` | `virtual_card_id`, `pin`(encrypted), `confirm_pin`, `identity_verify_token` | — |
| Reset PIN | POST | `/ppc/card/v1/reset-pin` | `virtual_card_id`, `pin`, `identity_verify_token` | 调 APIPTR 解锁 PIN |

- PIN 字段必加密传输。
- YSE Authorization 返回 `ResponseCode=75` 表示 PIN locked，需走 Reset 流程解锁。

## 卡详情查看

| 操作 | Method | Path（推断） | 关键字段 | 备注 |
|---|---|---|---|---|
| 查看卡明细 | GET | `/ppc/card/v1/detail` | `virtual_card_id`, `identity_verify_token` | — |
| 查看卡号 | GET | `/ppc/card/v1/pan` | `virtual_card_id`, `identity_verify_token` | 走 YSE 查询接口 |

- 所有敏感字段读取必须携带有效 `identity_verify_token`，失效 token 必拒。

## 锁卡 / 解锁 / 替换 / 关闭

| 操作 | Method | Path（推断） | 关键字段 | 幂等键 / 限制 |
|---|---|---|---|---|
| 锁卡 | POST | `/ppc/card/v1/lock` | `virtual_card_id`, `identity_verify_token` | `virtual_card_id + operate_session_id`（弱网防重复，BUG-6548）|
| 解锁卡 | POST | `/ppc/card/v1/unlock` | `virtual_card_id`, `identity_verify_token` | 同上（BUG-6554）|
| 替换卡 | POST | `/ppc/card/v1/replace` | `virtual_card_id`, `identity_verify_token` | 累计 ≤ 3 次 |
| 关闭卡（用户）| POST | `/ppc/card/v1/close` | `virtual_card_id`, `identity_verify_token`, `close_reason` | `virtual_card_id + close_session_id` |

- 关闭前必须余额清零，否则 `NON_ZERO_BALANCE`（资损用例必出）。
- 在 `INVALID_CARD_STATUS` 状态（已销卡 / 申请中 / Closing 中）下操作必拒。

## 实体卡申请、跟踪与激活

| 操作 | Method | Path（推断） | 关键字段 | 备注 |
|---|---|---|---|---|
| 实体卡申请初始化 | POST | `/ppc/card/v1/init-apply-physical` | `virtual_card_id` | 返回默认地址 + 名称 |
| 实体卡申请提交 | POST | `/ppc/card/v1/apply-physical` | `virtual_card_id`, `card_holder_name`(≤25), `delivery_address`, `card_style`(Standard/Metal) | 关闭未支付旧订单 |
| 跟踪实体卡 | GET | `/ppc/card/v1/tracking-physical-card-order` | `order_id` | 字段：`mobilePhoneNumber`(BUG-6892), `fees`(BUG-6893) |
| 激活实体卡 | POST | `/ppc/card/v1/activate` | `virtual_card_id`, `proxy_number` | 卡状态校验 = `UNACTIVATED` |

- 实体卡走 `apply-physical → 支付 → 制卡 → 配送 → activate` 全链路；配送状态由 [[ppc-api-card-network-inbound]] 中的 Jeebly/USP 回调驱动。
- `card_holder_name` 长度上限 25。

## 幂等键汇总

- `apply-virtual`：`member_id + card_type + session_id`
- `lock` / `unlock`：`virtual_card_id + operate_session_id`
- `close`：`virtual_card_id + close_session_id`
- 重复请求必须返回相同结果且 DB 不创建新记录。

## 相关错误码（本域常见）

- `INVALID_CARD_STATUS`、`NON_ZERO_BALANCE`、`VIRTUAL_CARD_NOT_EXIST`、`VIRTUAL_CARD_TYPE_NOT_EXIST`
- `KYC_NOT_VERIFIED`、`IDENTITY_VERIFY_FAILED`
- `PROCESSING_EXCEPTION`、`SYSTEM_EXCEPTION`
- 完整列表与触发场景见 [[ppc-api-error-codes]]。

## 串联用例参考

- 5-API 链路：申请 → 激活 → 锁 → 解锁 → 关闭。
- 6-API 链路：申请实体卡 → 支付 → 制卡 → 配送 → 激活（涉及 [[ppc-api-transaction]] 与 [[ppc-api-card-network-inbound]]）。
- 用例生成方法、覆盖度与边界规则见 [[ppc-api-test-case-generation-hints]]。
