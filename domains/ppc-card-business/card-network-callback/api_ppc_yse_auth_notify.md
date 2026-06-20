---
id: api_ppc_yse_auth_notify
object_type: API
domain: ppc-card-business
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- inbound
- callback
- yse
- authorization
subdomain: card-network-callback
module: yse-notify
sensitivity: normal
name: YSE授权回调接口
aliases:
- Authorization Notify
- YSE Auth Inbound
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
YSE/Jaywan 卡组织授权报文入向回调接口。当持卡人发生交易授权时，由 YSE/Jaywan 推送至 PPC，PPC 据此校验余额、写入授权流水、并设置 Pending Account。

## 路径/方法
- Method: `POST`
- Path（推断）: `/ppc/yse/notify/auth`
- 触发方: YSE/Jaywan
- 方向: 入向（Inbound from Card Network）

## 入参
原文未列出字段级 schema。源对应卡组织出向接口为 `Authorization (APIAUT)` 授权报文。

## 出参
原文未列出。

## 错误码
与该回调相关的关键状态/码：
- `ResponseCode=75`：PIN Locked（来自 YSE Authorization），表示用户 PIN 错误连续达上限。
- `PROCESSING_EXCEPTION`：上下游异常（YSE/trade/grc），需重试机制。
- `SYSTEM_EXCEPTION`：兜底系统异常。

## 测试校验点
- 处理动作覆盖：校验余额、写入授权流水、设置 Pending Account。
- 异步回调时序：必须覆盖乱序、重投、丢失、超时场景，验证幂等 + 兜底对账。
- PIN 锁定路径：`ResponseCode=75` 触发 PIN Locked 标记，与 PIN 解锁（APIPTR）流程联动回归。
- 与 Clearing 回调串联：Authorization 写入 Pending → 后续 Clearing 推动 Pending → Settle / Refund / Reversal。
- 上下游异常重试：`PROCESSING_EXCEPTION` 场景下重试机制必测。
- 系统异常降级：`SYSTEM_EXCEPTION` 兜底必测。
