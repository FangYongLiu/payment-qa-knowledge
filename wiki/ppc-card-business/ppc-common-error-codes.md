---
title: PPC通用错误码与测试提示
domain: ppc-card-business
kind: wiki_page
slug: ppc-common-error-codes
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags: []
---

# PPC通用错误码与测试提示

本页梳理 PPC API 在调用过程中常见的错误码、触发场景与对应的反向用例提示，并给出 API 测试用例的生成思路，供测试设计与 AI 生成用例时参考。完整 API 列表见 [[ppc-api-inventory]]。

## 通用错误码

| Code | 含义 | 触发场景 | 测试用例提示 |
|------|------|----------|--------------|
| `INVALID_CARD_STATUS` | 卡状态不允许该操作 | 已销卡操作 / 申请中激活 / Closing 中再次操作 | 反向状态用例必含 |
| `NON_ZERO_BALANCE` | 余额非零禁止关卡 | 关卡前未清零 | 必出资损用例 |
| `VIRTUAL_CARD_NOT_EXIST` | 虚拟卡不存在 | 错误 ID / 异步消息延迟 | — |
| `VIRTUAL_CARD_TYPE_NOT_EXIST` | 卡类型未配置 | BIN 路由异常 | — |
| `PROCESSING_EXCEPTION` | 处理异常 | 上下游异常（YSE/trade/grc） | 重试机制需测试 |
| `SYSTEM_EXCEPTION` | 系统异常 | 兜底 | 必测降级 |
| `KYC_NOT_VERIFIED` | KYC 未通过 | 申请卡前置校验 | 必测 |
| `IDENTITY_VERIFY_FAILED` | 核身失败 | 敏感操作前置 | 必测 |
| `ResponseCode 75` | PIN Locked（来自 YSE Authorization） | 用户 PIN 错误连续达上限 | PIN 解锁回归 |

## 错误码与典型 API 关联

- **状态类（`INVALID_CARD_STATUS`）**：覆盖 [[api_ppc_card_activate]]、[[api_ppc_card_lock]]、[[api_ppc_card_unlock]]、[[api_ppc_card_close]]、[[api_ppc_card_replace]] 等所有依赖卡当前状态的接口。
- **资损类（`NON_ZERO_BALANCE`）**：[[api_ppc_card_close]] 关卡前未清零必触发。
- **卡存在性（`VIRTUAL_CARD_NOT_EXIST` / `VIRTUAL_CARD_TYPE_NOT_EXIST`）**：所有以 `virtual_card_id` 为入参的接口均需测试错误 ID 与 BIN 路由异常。
- **核身类（`KYC_NOT_VERIFIED` / `IDENTITY_VERIFY_FAILED`）**：作用于 [[api_ppc_card_apply_virtual]]（KYC）以及所有要求 `identity_verify_token` 的敏感操作。
- **PIN Locked（`ResponseCode 75`）**：YSE 授权返回，需联动 [[api_ppc_card_reset_pin]]（调用 APIPTR 解锁）回归。
- **上下游异常类（`PROCESSING_EXCEPTION` / `SYSTEM_EXCEPTION`）**：需对所有 API 设计降级与重试用例。

## 测试用例生成提示

### API 覆盖度
- 每个 API 至少 1 条正向用例。
- 接口声明的每个错误码至少 1 条反向用例。

### 字段边界
- 金额：精度 / 边界 / 负数。
- 字符串：长度边界（如 `card_holder_name` ≤25）、特殊字符。
- 币种：合法 / 非法 ISO 码。
- PAN / CVV：必须加密传输。

### 幂等性
- 标注了幂等键的 API 必须有重复请求用例 → 同一幂等键二次请求返回相同结果、DB 不创建新记录。
- 典型幂等键 API：[[api_ppc_card_lock]]、[[api_ppc_card_unlock]]、[[api_ppc_card_close]]、[[api_ppc_card_apply_virtual]]。

### 串联用例
- **5-API 链路**：[[api_ppc_card_apply_virtual]] → [[api_ppc_card_activate]] → [[api_ppc_card_lock]] → [[api_ppc_card_unlock]] → [[api_ppc_card_close]]。
- **6-API 链路**（实体卡）：[[api_ppc_card_apply_physical]] → 支付 → 制卡 → 配送 → [[api_ppc_card_activate]]。

### 回调时序（异步）
- 必测乱序、重投、丢失、超时场景。
- 验证幂等 + 兜底对账。
- 涉及回调：[[api_ppc_yse_auth_notify]]、[[api_ppc_yse_clearing_notify]]、[[api_ppc_jeebly_delivery_status]]。

### 核身依赖
- 所有需要 `identity_verify_token` 的 API：失效 / 错误 token 必须拒绝。
- 例：[[api_ppc_card_set_pin]]、[[api_ppc_card_reset_pin]]、[[api_ppc_card_lock]]、[[api_ppc_card_unlock]]、[[api_ppc_card_replace]]、[[api_ppc_card_close]]。

## 用例规模估算

> 30+ APIs × 平均 4 条（happy + 错误码 + 边界 + 幂等） ≈ **~120 条** API 层用例。
