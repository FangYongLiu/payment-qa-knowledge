---
id: tbl_acquireii_t_event_param
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_event_param.md
tags:
- 事件
- KV
- 参数
subdomain: null
module: event
sensitivity: normal
name: 事件参数表 (t_event_param)
aliases:
- t_event_param
- acquireii.t_event_param
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

存储**事件（event）的扩展参数**，以 KV 结构（pkey/value）保存事件的附加信息，通过 `id` 关联事件主表（如 `t_stmt_event` 或其他事件表）。

在收单系统中，事件是异步通知或状态变更的载体，需要附带参数。典型场景：
- 订单状态变更事件 → 携带新旧状态参数
- 风控触发事件 → 携带风控分数、规则 ID 等参数
- 对账事件 → 携带对账批次、差异金额等参数

表名：`acquireii.t_event_param`，重要程度 ⭐⭐。

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `id` | bigint | ✅ | 联合主键，事件 ID（关联事件主表） |
| `pkey` | varchar(50) | ✅ | 联合主键，参数键 |
| `value` | varchar(200) | ✅ | 参数值 |

## 主键/索引

- PRIMARY：联合主键 `(id, pkey)`

## 校验点(QA 关注)

1. **pkey 由事件类型定义**：不同事件类型对应不同参数集，需按事件类型校验 pkey 命名与取值是否符合约定。
2. **没有时间字段**：本表不含时间列，要查询参数发生时间须回到事件主表。
3. **value 长度 200**：超长值需要拆分存储，避免被截断。
4. **关联完整性**：`id` 必须能在对应事件主表（如 `t_stmt_event`）中找到，避免出现孤立参数行。
5. **常见查询模式**：按 `id` 直接列出全部 pkey/value，或使用 `MAX(CASE WHEN pkey = ...)` 透视成列（如 old_status/new_status/reason）。
