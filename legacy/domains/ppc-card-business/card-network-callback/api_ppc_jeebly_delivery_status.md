---
id: api_ppc_jeebly_delivery_status
object_type: API
domain: ppc-card-business
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- 回调
- 入向
- 配送
- Jeebly
subdomain: card-network-callback
module: physical-card-delivery
sensitivity: normal
name: Jeebly配送状态回调接口
aliases:
- Jeebly Delivery Status
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures:
- BUG-8948
---

## 用途
Jeebly 配送服务回调 PPC，通知实体卡的配送状态变更（入向回调）。

## 路径/方法
- Method: POST
- Path（推断）: `/ppc/api/jeebly/delivery-status`
- 触发方: Jeebly

## 入参
原文未列出字段明细。仅明确状态枚举值：
- `Out for delivery`
- `Delivered`
- `Cancelled`
- `RTO Delivered`

## 出参
原文未提供。

## 错误码
原文未为本接口列出专属错误码。可参考 [[ppc-common-error-codes]] 中通用错误码：
- `PROCESSING_EXCEPTION`（上下游异常）
- `SYSTEM_EXCEPTION`（兜底）

已知缺陷：
- BUG-8948：`RTO Delivered` 状态处理报错。

## 测试校验点
- 四种状态各至少 1 条正向用例：`Out for delivery` / `Delivered` / `Cancelled` / `RTO Delivered`。
- `RTO Delivered` 必须回归 BUG-8948。
- 异步回调时序用例：乱序、重投、丢失、超时 → 验证幂等 + 兜底对账。
- 重复回调（同一 order 同一状态）→ 幂等，DB 不产生重复记录。
- 跨 API 串联：申请实体卡 → 支付 → 制卡 → 配送（本接口）→ 激活，作为 6-API 链路一环。
