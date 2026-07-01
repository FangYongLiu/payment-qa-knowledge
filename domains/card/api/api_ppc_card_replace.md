---
id: api_ppc_card_replace
object_type: API
domain: card
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- card-management
- virtual-card
subdomain: card-management
module: null
sensitivity: normal
name: 替换卡接口
aliases:
- Replace card
- /ppc/card/v1/replace
related_services:
- svc_ppc
---

## 用途
替换虚拟卡（生成新卡替代原卡）。累计调用次数限制 ≤ 3 次。

## 路径/方法
- Method: `POST`
- Path（推断，待后端确认）: `/ppc/card/v1/replace`
- 网关: CGS (Client Gateway Service) — App 调用
- API 文档: https://sim-admin.corp.test2pay.com/api-doc/

## 入参
| 字段 | 说明 |
|---|---|
| `virtual_card_id` | 虚拟卡 ID |
| `identity_verify_token` | 核身 token，敏感操作前置 |

## 出参
原文未明确列出出参字段，参考 API 文档（Smart-doc 自动生成）。

## 错误码
参考 [[ppc-common-error-codes]]，本接口可能涉及：
- `INVALID_CARD_STATUS` — 卡状态不允许替换（如已销卡 / 申请中 / Closing 中）
- `VIRTUAL_CARD_NOT_EXIST` — 虚拟卡不存在
- `IDENTITY_VERIFY_FAILED` — 核身失败
- `PROCESSING_EXCEPTION` — 上下游处理异常（YSE 等）
- `SYSTEM_EXCEPTION` — 系统异常兜底

## 测试校验点
- **正向用例**：合法 `virtual_card_id` + 有效 `identity_verify_token` 替换成功。
- **次数限制**：累计替换次数 ≤ 3 次；第 4 次调用必须被拒绝。
- **核身依赖**：失效 / 缺失 `identity_verify_token` 必拒。
- **状态反向**：卡状态为已销卡 / 申请中 / Closing 中等不允许操作的状态 → 返回 `INVALID_CARD_STATUS`。
- **不存在卡**：错误 `virtual_card_id` → `VIRTUAL_CARD_NOT_EXIST`。
- **上下游异常**：YSE 异常路径 → `PROCESSING_EXCEPTION`，验证重试机制。
- **串联用例**：可纳入卡生命周期链路用例验证替换后新卡可用、原卡失效。
