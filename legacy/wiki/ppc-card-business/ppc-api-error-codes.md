---
title: PPC通用错误码与测试提示
domain: ppc-card-business
kind: wiki_page
slug: ppc-api-error-codes
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2133098640
tags: []
---

# PPC通用错误码与测试提示

本页汇总 PPC API 在错误返回时使用的通用错误码、典型触发场景，以及由此衍生的反向测试用例提示，供测试用例设计与回归覆盖参考。

## 通用错误码列表

| Code | 含义 | 触发场景 | 测试用例提示 |
|---|---|---|---|
| `INVALID_CARD_STATUS` | 卡状态不允许该操作 | 已销卡再操作 / 申请中执行激活 / Closing 中重复操作 | 反向状态用例必含 |
| `NON_ZERO_BALANCE` | 余额非零禁止关卡 | 关卡前未清零 | 必出资损用例 |
| `VIRTUAL_CARD_NOT_EXIST` | 虚拟卡不存在 | 错误 ID / 异步消息延迟 | — |
| `VIRTUAL_CARD_TYPE_NOT_EXIST` | 卡类型未配置 | BIN 路由异常 | — |
| `PROCESSING_EXCEPTION` | 处理异常 | 上下游异常（YSE/trade/grc） | 重试机制需测试 |
| `SYSTEM_EXCEPTION` | 系统异常 | 兜底 | 必测降级 |
| `KYC_NOT_VERIFIED` | KYC 未通过 | 申请卡前置校验 | 必测 |
| `IDENTITY_VERIFY_FAILED` | 核身失败 | 敏感操作前置 | 必测 |
| `ResponseCode 75` | PIN Locked（来自 YSE Authorization） | 用户 PIN 错误连续达上限 | PIN 解锁回归 |

## 反向用例设计要点

- **状态机覆盖**：对返回 `INVALID_CARD_STATUS` 的 API（锁/解锁/关闭/激活/替换等），需对每个非法前置状态各设计 1 条反向用例。
- **资损相关**：`NON_ZERO_BALANCE` 属于资损红线，关卡流程必出该反向用例。
- **上下游异常**：`PROCESSING_EXCEPTION` 需配合下游 mock（YSE/trade/grc）异常注入并验证重试。
- **兜底降级**：`SYSTEM_EXCEPTION` 必测兜底返回与告警链路。
- **核身令牌**：所有需 `identity_verify_token` 的 API，失效/伪造 token 必返回 `IDENTITY_VERIFY_FAILED` 且必拒。
- **PIN Locked**：YSE Authorization 返回 `ResponseCode=75` 时，需联动调用 APIPTR 的 PIN 解锁回归用例（参见 [[ppc-api-card-network-inbound]]）。

## 与其他页的关系

- 卡管理 API 的字段与状态前置条件见 [[ppc-api-card-management]]。
- 入向回调（Authorization / Clearing / PIN Lock）触发的错误码场景见 [[ppc-api-card-network-inbound]]。
- 用例生成的整体策略（覆盖度、边界、幂等、串联）见 [[ppc-api-test-case-generation-hints]]。
