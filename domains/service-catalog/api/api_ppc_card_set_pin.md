---
id: api_ppc_card_set_pin
object_type: API
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- card-management
- pin
- sensitive
subdomain: card-management
module: null
sensitivity: normal
name: 设置卡PIN接口
aliases:
- Set PIN
related_services:
- svc_ppc
---

## 用途
设置 PPC 虚拟卡的 PIN 码。属于敏感操作，需要核身校验。由 App 调用，经 CGS (gp024_cgs) 网关进入。

## 路径/方法
- Method: POST
- Path（推断，待后端确认）: `/ppc/card/v1/set-pin`
- 调用方: App
- 网关: CGS (Client Gateway Service)

## 入参
| 字段 | 说明 |
|---|---|
| `virtual_card_id` | 虚拟卡 ID |
| `pin` | PIN（加密传输） |
| `confirm_pin` | 确认 PIN |
| `identity_verify_token` | 核身 token |

## 出参
原文未声明具体返回字段。返回结果遵循通用 API 返回结构（参见 API 文档：https://sim-admin.corp.test2pay.com/api-doc/）。

## 错误码
本 API 可能命中的通用错误码（详见 [[ppc-common-error-codes]]）：
- `INVALID_CARD_STATUS` — 卡状态不允许该操作
- `VIRTUAL_CARD_NOT_EXIST` — 虚拟卡不存在
- `IDENTITY_VERIFY_FAILED` — 核身失败
- `KYC_NOT_VERIFIED` — KYC 未通过
- `PROCESSING_EXCEPTION` — 处理异常（上下游 YSE 等）
- `SYSTEM_EXCEPTION` — 系统异常兜底

## 测试校验点
- 正向用例：合法 `virtual_card_id` + 加密 `pin` + `confirm_pin` 一致 + 有效 `identity_verify_token` → 设置成功。
- 字段边界：
  - `pin` 必须加密传输（敏感字段）。
  - `pin` 与 `confirm_pin` 不一致 → 拒绝。
- 反向用例（每个错误码至少 1 条）：
  - 无效 / 失效 `identity_verify_token` → 必拒（`IDENTITY_VERIFY_FAILED`）。
  - `virtual_card_id` 不存在 → `VIRTUAL_CARD_NOT_EXIST`。
  - 卡状态非法（已销卡 / Closing 中等）→ `INVALID_CARD_STATUS`。
  - 未通过 KYC → `KYC_NOT_VERIFIED`。
  - 上下游异常 → `PROCESSING_EXCEPTION`，验证重试机制。
- 串联：与 [[api_ppc_card_apply_virtual]]（申请虚拟卡）后接此接口设置 PIN，PIN 错误连续达上限后由 YSE Authorization 返回 `ResponseCode=75`（PIN Locked），由 [[api_ppc_card_reset_pin]] 调 APIPTR 解锁回归。
- 核身依赖：所有需 `identity_verify_token` 的 API → 失效 token 必拒。
