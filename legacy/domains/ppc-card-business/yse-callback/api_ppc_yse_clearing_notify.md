---
id: api_ppc_yse_clearing_notify
object_type: API
domain: ppc-card-business
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- yse
- callback
- inbound
- clearing
subdomain: yse-callback
module: inbound-notify
sensitivity: normal
name: YSE清算回调接口
aliases:
- Clearing Notify
- Settle Notify
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
YSE/Jaywan 卡组织清算/结算入向回调接口。接收清算事件后，将本地交易由 Pending Account 流转至 Settle / Refund / Reversal 终态，完成账务最终化。

## 路径/方法
- Method: POST
- Path（推断）: `/ppc/yse/notify/clearing`
- 触发方: YSE / Jaywan

## 入参
原文未声明清算回调具体字段（待后端确认）。语义上需包含：
- 关联授权流水的标识（用于匹配 Pending Account 记录）
- 清算结果类型：Settle / Refund / Reversal
- 金额、币种等清算明细

## 出参
原文未明确出参结构。需返回幂等可识别的应答，支持卡组织重投。

## 错误码
本接口未单独声明专属错误码。可复用通用错误码：
- `PROCESSING_EXCEPTION`：上下游（YSE/trade/grc）异常
- `SYSTEM_EXCEPTION`：兜底系统异常
- `VIRTUAL_CARD_NOT_EXIST`：异步消息延迟或卡不存在导致匹配失败

## 测试校验点
- 处理动作正确性：Pending → Settle / Refund / Reversal 三种终态分支均需覆盖。
- 异步时序用例（必测）：
  - 乱序：Clearing 早于 Authorization 到达
  - 重投：相同清算事件多次推送 → 幂等，DB 不重复入账
  - 丢失：Clearing 未到达 → 兜底对账机制触发
  - 超时：处理超时后重试逻辑
- 与 `api_ppc_yse_auth_notify` 串联：授权写入 Pending Account 后，Clearing 必须能正确匹配并流转。
- 错误码反向用例：上下游异常 → `PROCESSING_EXCEPTION`，需验证重试机制。
- 资损相关：Refund / Reversal 分支金额方向、账务一致性必测。
- 参考 `ppc-SD-3-Transaction` 中 Authorization / Clearing / Reversal 的详细账务规则。
