---
title: PPC API测试用例生成指引
domain: ppc-card-business
kind: wiki_page
slug: ppc-api-test-case-generation-hints
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2133098640
tags: []
---

# PPC API测试用例生成指引

本页提炼 PPC API 测试用例的生成规则，覆盖 API 覆盖度、字段边界、幂等性、串联链路、回调时序与核身依赖六大维度，供 AI 或 QA 推导用例。基础接口清单见 [[ppc-api-inventory-overview]]。

## API 覆盖度

- 每个 API 至少 1 条正向（happy path）用例。
- 每个声明的错误码至少 1 条反向用例（错误码清单见 [[ppc-api-error-codes]]）。
- 卡管理 API 列表见 [[ppc-api-card-management]]，交易/账务 API 见 [[ppc-api-transaction]]。

## 字段边界

- **金额**：精度、上下界、负数。
- **字符串**：长度边界、特殊字符（如 `card_holder_name` ≤25）。
- **币种**：合法 / 非法 ISO 代码。
- **敏感字段**：PAN、CVV、PIN 必须加密传输。

## 幂等性

- 每个标注幂等键的 API 必出 1 条重复请求用例：返回结果一致、DB 不重复落单。
- 典型幂等键：
  - 申请虚拟卡：`member_id + card_type + session_id`
  - 锁卡 / 解锁卡：`virtual_card_id + operate_session_id`（弱网防重复，BUG-6548 / BUG-6554）
  - 关卡：`virtual_card_id + close_session_id`
- 异步回调（[[ppc-api-card-network-inbound]]）必测重投幂等。

## 串联链路用例

- **5-API 链路（虚拟卡）**：申请 → 激活 → 锁 → 解锁 → 关闭。
- **6-API 链路（实体卡）**：申请实体卡 → 支付 → 制卡 → 配送 → 激活。
- 链路用例需校验跨服务状态一致性（卡状态、账务、YSE 同步）。

## 回调时序（异步）

针对入向回调（[[ppc-api-card-network-inbound]]）必测：

- 乱序投递（如 Clearing 先于 Authorization）
- 重投（重复回调）
- 丢失（依赖兜底对账）
- 超时
- 验证点：幂等处理 + 对账兜底机制。

## 核身依赖

- 所有需 `identity_verify_token` 的 API（设置/Reset PIN、查看卡明细、查看卡号、锁卡、解锁卡、替换卡、关闭卡等）：
  - 失效 / 错误 / 过期 token → 必须拒绝。
  - 错误码 `IDENTITY_VERIFY_FAILED` 反向用例必出。
- KYC 前置：申请卡时未通过 KYC → `KYC_NOT_VERIFIED`，必测。

## 特殊业务规则用例

- **关卡**：余额非零禁止关闭 → `NON_ZERO_BALANCE`，必出资损用例。
- **替换卡**：累计 ≤ 3 次，第 4 次必拒。
- **激活实体卡**：仅当卡状态 = `UNACTIVATED` 才允许。
- **PIN Locked**：YSE Authorization 返回 `ResponseCode=75` → 调用 APIPTR 解锁，必做回归。
- **FX 试算**：弱网键盘关闭后不应再调用（BUG-6529）。
- **Jeebly Delivery Status**：覆盖 Out for delivery / Delivered / Cancelled / RTO Delivered（BUG-8948 RTO 处理需回归）。

## 用例规模估算

- 30+ APIs × 平均 4 条（happy + 错误码 + 边界 + 幂等）≈ **~120 条** API 层用例。
- 不含跨链路 / 异步时序的额外组合用例。

## 关联页面

- 网关与调用方区分：[[ppc-api-gateways]]
- 错误码字典：[[ppc-api-error-codes]]
- 入向回调清单：[[ppc-api-card-network-inbound]]
