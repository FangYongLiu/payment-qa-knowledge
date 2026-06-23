---
id: api_ppc_card_reset_pin
object_type: API
domain: ppc-card-business
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- card
- pin
- APIPTR
subdomain: card-management
module: null
sensitivity: normal
name: 重置卡PIN接口
aliases:
- Reset PIN
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
通过调用卡组织 APIPTR (PIN Tries Reset) 解锁并重置虚拟卡的 PIN，用于用户 PIN 连续输错被锁（YSE Authorization ResponseCode=75）后的恢复操作。

## 路径/方法
- Method: POST
- Path（推断，待后端确认）: `/ppc/card/v1/reset-pin`
- 调用方: App
- 网关: CGS (gp024_cgs)

## 入参
| 字段 | 说明 |
|---|---|
| `virtual_card_id` | 虚拟卡 ID |
| `pin` | 新 PIN（加密传输） |
| `identity_verify_token` | 核身令牌（敏感操作前置） |

注：处理动作为调用 APIPTR 解锁 PIN。

## 出参
原文未列出具体出参字段。

## 错误码
- `INVALID_CARD_STATUS`：卡状态不允许该操作
- `VIRTUAL_CARD_NOT_EXIST`：虚拟卡不存在
- `IDENTITY_VERIFY_FAILED`：核身失败
- `PROCESSING_EXCEPTION`：上下游（YSE）处理异常
- `SYSTEM_EXCEPTION`：系统异常兜底
- 上游 ResponseCode=75：PIN Locked（来自 YSE Authorization，触发 reset 场景）

## 测试校验点
- 正向：YSE Authorization 返回 ResponseCode=75（PIN Locked）后，调用本接口成功调 APIPTR 解锁并重置 PIN。
- 反向错误码：每个声明错误码至少 1 条反向用例。
- 字段边界：`pin` 必加密传输；新旧 PIN 规则边界。
- 核身依赖：`identity_verify_token` 失效 / 缺失必拒。
- PIN 解锁回归：ResponseCode=75 → reset → 后续 Authorization 不再 75。
- 上下游异常：YSE/APIPTR 异常时返回 `PROCESSING_EXCEPTION`，重试机制可用。
