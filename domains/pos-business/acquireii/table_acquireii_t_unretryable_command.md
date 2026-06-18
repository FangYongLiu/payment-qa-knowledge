---
id: tbl_acquireii_t_unretryable_command
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_unretryable_command.md
tags:
- acquireii
- command
- unretryable
subdomain: acquireii
module: command
sensitivity: normal
name: 不可重试指令表
aliases:
- t_unretryable_command
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

记录**不允许重试**的异步指令。某些指令一旦失败就不能再次执行，因为重复执行会带来资金或状态风险，必须人工介入处理。

**典型场景**：
- **支付指令**：重复执行可能导致用户多扣款
- **退款指令**：重复执行可能导致多退款
- **冲正指令**：重复执行可能导致状态错乱

**与 `t_retryable_command` 区分**：
- `t_retryable_command`：失败后会重试（如通知商户、对账）
- `t_unretryable_command`：失败后不重试，需要人工介入

表名：`acquireii.t_unretryable_command`，主键 `id`。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `id` | bigint | ✅ | 主键，对应 `t_command.id` |
| `category` | varchar(50) | ✅ | 指令类别（支付/退款/冲正等） |
| `external_order_id` | varchar(100) |  | 外部订单 ID |
| `status` | varchar(32) |  | 状态（如 RUNNING、FAILED） |
| `memo` | varchar(100) |  | 备注 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `id` | 主键 |
| `i_uc_eoi` | `external_order_id` | 按外部订单查询 |
| `i_urcmd_ct` | `created_time` | 按时间扫描 |

**关联表**：
- `t_command`（1:1，关联字段 `id`）
- `t_command_param`（1:N，关联字段 `id`）

## 校验点(QA 关注)

1. **失败必须告警**：`status = 'FAILED'` 意味着资金/状态可能错乱，需要人工介入；近 1 小时内的失败记录应被高优先级告警捕获。
2. **处理中超时检测**：`status = 'RUNNING'` 且 `created_time` 超过 5 分钟未更新，可能已卡死，需要排查。
3. **不可随意重置状态**：手动修改 `status` 可能导致指令被重复执行，引发多扣款/多退款。
4. **与重试表互斥**：同一条指令应只存在于 `t_retryable_command` 或 `t_unretryable_command` 之一，不应同时出现。
5. **类别覆盖**：`category` 应覆盖支付调用、退款调用、冲正调用等涉及资金的操作类型。
6. **data_version 乐观锁**：更新时应校验 `data_version` 防并发覆盖。
