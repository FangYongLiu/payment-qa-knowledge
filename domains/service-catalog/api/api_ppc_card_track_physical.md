---
id: api_ppc_card_track_physical
object_type: API
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- card
- physical-card
- delivery
- tracking
subdomain: card-management
module: null
sensitivity: normal
name: 跟踪实体卡配送接口
aliases:
- Track delivery
related_services:
- svc_ppc
---

## 用途
查询实体卡配送状态（订单跟踪）。App 端通过 `order_id` 查询某笔实体卡订单的配送进度。

## 路径/方法
- Method: `GET`
- Path（推断，待后端确认）: `/ppc/card/v1/tracking-physical-card-order`
- 网关: CGS (gp024_cgs)
- 调用方: App

## 入参
| 字段 | 说明 |
|---|---|
| order_id | 实体卡订单 ID |

## 出参
返回实体卡订单的配送跟踪信息。已知字段：
- `mobilePhoneNumber`（关联 BUG-6892）
- `fees`（关联 BUG-6893）

> 详细字段以 Smart-doc 实时文档为准：https://sim-admin.corp.test2pay.com/api-doc/

## 错误码
通用错误码（参见 [[ppc-common-error-codes]]）：
- `VIRTUAL_CARD_NOT_EXIST` — 错误 ID / 异步消息延迟
- `PROCESSING_EXCEPTION` — 上下游异常
- `SYSTEM_EXCEPTION` — 兜底

## 测试校验点
- 正向用例：合法 `order_id` 返回正确配送状态。
- 反向用例：非法 / 不存在的 `order_id` 返回相应错误码。
- 字段回归：
  - `mobilePhoneNumber` 字段返回正确（BUG-6892 回归）。
  - `fees` 字段返回正确（BUG-6893 回归）。
- 串联用例：作为 6-API 链路的一环（physical-apply → pay → produce → ship → activate）中"ship"阶段查询。
- 配送状态联动：与 [[api_ppc_jeebly_delivery_status]] 回调状态（Out for delivery / Delivered / Cancelled / RTO Delivered）一致性校验。
