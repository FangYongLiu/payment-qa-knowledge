---
id: api_ppc_card_close
object_type: API
domain: ppc-card-business
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- card-management
- user-initiated
- idempotent
subdomain: card-management
module: null
sensitivity: normal
name: 关闭卡接口
aliases:
- Close card
- 关闭卡（用户）
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
用户主动关闭虚拟卡。需身份核身通过，且卡余额必须为零。

## 路径/方法
- Method: POST
- Path（推断，待后端确认）: `/ppc/card/v1/close`
- 调用方: App
- 网关: CGS (gp024_cgs)

## 入参
| 字段 | 说明 |
|---|---|
| `virtual_card_id` | 虚拟卡 ID |
| `identity_verify_token` | 核身令牌（敏感操作前置） |
| `close_reason` | 关闭原因 |

幂等键 / Idempotent Key: `virtual_card_id + close_session_id`

## 出参
原文未声明出参字段（详见 Smart-doc 接口文档 https://sim-admin.corp.test2pay.com/api-doc/）。

## 错误码
| Code | 触发场景 |
|---|---|
| `INVALID_CARD_STATUS` | 卡状态不允许该操作（已销卡 / 申请中 / Closing 中再次操作） |
| `NON_ZERO_BALANCE` | 关卡前余额未清零 |
| `VIRTUAL_CARD_NOT_EXIST` | 错误 ID / 异步消息延迟 |
| `IDENTITY_VERIFY_FAILED` | 核身失败 |
| `PROCESSING_EXCEPTION` | 上下游异常（YSE/trade/grc） |
| `SYSTEM_EXCEPTION` | 兜底系统异常 |

## 测试校验点
- 正向：核身通过 + 余额=0 + 卡状态合法 → 关闭成功。
- 反向状态用例：已销卡 / Closing 中 / 申请中 状态再次调用 → 返回 `INVALID_CARD_STATUS`。
- 资损用例（必出）：余额非零调用关卡 → 返回 `NON_ZERO_BALANCE`，禁止关卡。
- 核身：`identity_verify_token` 失效/缺失 → 必拒（`IDENTITY_VERIFY_FAILED`）。
- 幂等性：同一 `virtual_card_id + close_session_id` 重复请求 → 返回相同结果，DB 不创建新记录。
- 不存在卡：错误 `virtual_card_id` → 返回 `VIRTUAL_CARD_NOT_EXIST`。
- 串联链路：申请 → 激活 → 锁 → 解锁 → 关闭（5-API 链路）末环节。
- 上下游异常：`PROCESSING_EXCEPTION` 重试机制需测试；`SYSTEM_EXCEPTION` 必测降级。
