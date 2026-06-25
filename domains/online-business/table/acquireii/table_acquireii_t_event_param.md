---
id: tbl_acquireii_t_event_param
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
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
related_services:
- svc_acquireii
---

## 用途

`acquireii.t_event_param` 用于存储**事件（event）的扩展参数**，以 KV 结构（pkey/value）保存事件的附加信息，通过 `id` 关联事件主表（如 `t_stmt_event` 或其他事件表）。

在收单系统中，事件是异步通知或状态变更的载体，主表只能容纳固定结构的核心字段，而事件类型千差万别需要附带的参数集合不固定，因此通过本表以纵表形式承载可变参数。

典型场景：
- 订单状态变更事件 → 携带新旧状态参数（old_status / new_status / reason）
- 风控触发事件 → 携带风控分数、规则 ID 等参数
- 对账事件 → 携带对账批次、差异金额等参数

表名：`acquireii.t_event_param`，重要程度 ⭐⭐。

## 在交易链路中的位置

收单交易主链路：下单（`t_acquire_order`）→ 支付/退款/撤销/冲正等子单 → 触发各类事件（落库到事件主表）→ 事件扩展参数落库到 `t_event_param`。

本表属于**事件层的旁路扩展表**，不参与交易主流程的强一致写入，但在对账、风控复盘、状态机回溯等场景中是关键数据来源。它与 `t_command_param` 之于 `t_command` 的关系类似，都是 KV 扩展模式。

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `id` | bigint | ✅ | 联合主键，事件 ID（关联事件主表，如 `t_stmt_event.id`） |
| `pkey` | varchar(50) | ✅ | 联合主键，参数键 |
| `value` | varchar(200) | ✅ | 参数值 |

## 主键 / 索引

- PRIMARY：联合主键 `(id, pkey)`，天然防止同一事件下同 key 重复写入。

## 与关联表的关系

| 关联表 | 关联字段 | 关系说明 |
|--------|---------|---------|
| `t_stmt_event` | `t_event_param.id = t_stmt_event.id` | 对账事件主表，本表为其参数明细 |
| 其他事件主表 | `id` | 同上，按事件类型决定主表 |
| `t_acquire_order` 及子订单 | 通过事件主表的业务单号间接关联 | 用于回溯事件参数到具体交易 |
| `t_command_param` | 结构同构 | 都是 KV 扩展模式，QA 检查思路可复用 |

## 校验点（QA 关注）

1. **pkey 由事件类型定义**：不同事件类型对应不同参数集，需按事件类型校验 pkey 命名与取值是否符合约定。
2. **没有时间字段**：本表不含任何时间列，查询参数发生时间须回到事件主表（如 `t_stmt_event` 的事件时间字段）。
3. **value 长度 200**：超长值需要拆分存储或上游裁剪，QA 验证时关注是否被截断。
4. **关联完整性**：`id` 必须能在对应事件主表中找到，避免出现孤立参数行；同时事件主表存在但本表缺关键 pkey 也属异常。
5. **联合主键唯一性**：同一 `id` 下相同 `pkey` 不应重复，重复写入会因主键冲突失败。
6. **常见查询模式**：
   - 按 `id` 直接列出全部 pkey/value 做参数审查；
   - 使用 `MAX(CASE WHEN pkey = 'xxx' THEN value END)` 透视成列（如 old_status / new_status / reason），便于和事件主表 join 后输出宽表。

## QA 落库检查要点

- 商户交易落库检查（`scn_merchant_transaction_db_check`）覆盖事件类用例时，需联查事件主表 + `t_event_param`，验证：
  1. 事件主表是否生成对应记录；
  2. 本表参数集是否齐全（按事件类型对照预期 pkey 列表）；
  3. value 内容是否符合业务预期（如状态值、金额、原因码）；
  4. 不存在孤立参数行（`id` 在主表无对应记录）。
- 对账、状态机变更、风控触发类场景，建议把 `t_event_param` 作为事实补强证据落入用例断言。
