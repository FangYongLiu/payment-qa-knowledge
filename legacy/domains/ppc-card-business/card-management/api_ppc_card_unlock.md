---
id: api_ppc_card_unlock
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
name: 解锁卡接口
aliases:
- Unlock card
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures:
- BUG-6554
---

## 用途
解锁此前被锁定的虚拟卡，恢复卡的可用状态。由 App 端调用，CGS 网关入口。

## 路径/方法
- Method: `POST`
- Path（推断，待后端确认）: `/ppc/card/v1/unlock`
- 网关: CGS (Client Gateway Service, gp024_cgs)
- 调用方: App

## 入参
| 字段 | 说明 |
| --- | --- |
| `virtual_card_id` | 虚拟卡 ID |
| `identity_verify_token` | 核身 token，敏感操作前置 |

## 出参
原文未明确出参字段（详见 Smart-doc：https://sim-admin.corp.test2pay.com/api-doc/）。

## 错误码
- `INVALID_CARD_STATUS` — 卡状态不允许解锁（如已销卡 / Closing 中）
- `VIRTUAL_CARD_NOT_EXIST` — 虚拟卡不存在
- `IDENTITY_VERIFY_FAILED` — 核身失败
- `PROCESSING_EXCEPTION` — 上下游处理异常
- `SYSTEM_EXCEPTION` — 系统兜底异常

## 测试校验点
- **正向**：已锁定卡执行 unlock，返回成功，卡状态恢复为可用。
- **反向状态**：对未锁定 / 已销卡 / Closing 中的卡 unlock → `INVALID_CARD_STATUS`。
- **幂等性**：幂等键 = `virtual_card_id + operate_session_id`，弱网重复请求需返回相同结果，DB 不重复处理（参考 BUG-6554）。
- **核身依赖**：失效或缺失 `identity_verify_token` 必拒 → `IDENTITY_VERIFY_FAILED`。
- **不存在卡**：错误 `virtual_card_id` → `VIRTUAL_CARD_NOT_EXIST`。
- **串联**：apply → activate → lock → **unlock** → close 5-API 链路覆盖。
- **异常重试**：上下游（YSE）异常时 `PROCESSING_EXCEPTION` 重试机制需验证。
