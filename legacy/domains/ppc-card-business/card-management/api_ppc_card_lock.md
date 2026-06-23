---
id: api_ppc_card_lock
object_type: API
domain: ppc-card-business
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- card-management
- idempotent
subdomain: card-management
module: null
sensitivity: normal
name: 锁卡接口
aliases:
- Lock card
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures:
- BUG-6548
---

## 用途
锁定虚拟卡，禁止后续授权交易。属于卡管理 API，调用方为 App。需结合弱网防重幂等键避免重复锁卡（参见 BUG-6548）。

## 路径/方法
- Method: POST
- Path（推断，待后端确认）: `/ppc/card/v1/lock`
- 网关: CGS (gp024_cgs)

## 入参
| 字段 | 说明 |
|---|---|
| `virtual_card_id` | 虚拟卡 ID |
| `identity_verify_token` | 核身 token，敏感操作前置必填 |

幂等键 / Idempotent Key: `virtual_card_id + operate_session_id`（弱网防重复，BUG-6548）

## 出参
原文未列出具体出参字段，遵循 PPC 通用响应结构。

## 错误码
- `INVALID_CARD_STATUS` — 卡状态不允许该操作（如已销卡 / 申请中 / Closing 中）
- `VIRTUAL_CARD_NOT_EXIST` — 虚拟卡不存在
- `IDENTITY_VERIFY_FAILED` — 核身失败
- `PROCESSING_EXCEPTION` — 上下游处理异常
- `SYSTEM_EXCEPTION` — 系统异常兜底

## 测试校验点
- 正向：合法 `virtual_card_id` + 有效 `identity_verify_token` → 锁卡成功。
- 反向状态：已销卡 / Closing 中 / 已锁状态再次锁卡 → 返回 `INVALID_CARD_STATUS`。
- 不存在卡：错误 `virtual_card_id` → `VIRTUAL_CARD_NOT_EXIST`。
- 核身：失效 / 缺失 `identity_verify_token` 必拒 → `IDENTITY_VERIFY_FAILED`。
- 幂等性（BUG-6548 弱网防重复）：相同 `virtual_card_id + operate_session_id` 重复请求 → 返回相同结果，DB 不重复写入。
- 串联用例：申请 → 激活 → **锁** → 解锁 → 关闭（5-API 链路）。
- 上下游异常：YSE 异常时返回 `PROCESSING_EXCEPTION`，验证重试机制。
