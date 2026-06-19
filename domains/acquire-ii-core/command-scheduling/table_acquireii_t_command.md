---
id: tbl_acquireii_t_command
object_type: Table
domain: acquire-transaction
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_command.md
tags:
- 指令调度
- 异步执行
- 核心表
subdomain: command-scheduling
module: null
sensitivity: normal
name: 指令表 t_command
aliases:
- acquireii.t_command
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_command_param
- tbl_acquireii_t_deposit_order
- tbl_acquireii_t_event_param
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_retryable_command
- tbl_acquireii_t_reversal_order
- tbl_acquireii_t_revoke_order
- tbl_acquireii_t_stmt_event
- tbl_acquireii_t_unretryable_command
- tbl_acquireii_t_void_order
related_scenarios:
- scn_merchant_transaction_db_check
- scn_mit_autodebit
- scn_payby_withdraw_core_cases
- scn_vam_iban_fitnesse_notify
- scn_withdraw_to_bank_main_flows
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
收单系统的**异步指令调度核心表**（`acquireii.t_command`）。所有需要异步执行的操作都会在此表生成一条指令记录，由调度系统消费执行。所有的发出 id（`current_cmd_id` / `last_cmd_id`）都从这里读。

典型场景：
- 创建订单后，发出"调用渠道"指令（CHANNEL_CALL）
- 退款/撤销后，发出"通知商户"指令（NOTIFY）
- 定时任务，发出"对账"指令（RECONCILE）

## 在交易链路中的位置
```
业务订单表 (t_acquire_order / t_refund_order / t_reversal_order / t_revoke_order / t_void_order / t_deposit_order)
   │  current_cmd_id ──────────►  t_command (本表，调度核心)
   │                                 │
   │                                 ├── 1:N ──► t_command_param   （指令参数）
   │                                 ├── 1:1 ──► t_retryable_command （可重试扩展）
   │                                 └── 1:1 ──► t_unretryable_command（不可重试扩展）
   │
   └── 指令执行后产生事件 ─────────►  t_stmt_event / t_event_param
```
指令是订单状态推进的驱动者：订单写入后挂一个 `current_cmd_id` 指向 t_command，调度器拉起该指令完成渠道调用、商户通知、对账等动作，并回写订单状态。

## 关键列
**主键与指令信息**
- `id` bigint，主键，指令 ID（被各订单表的 `current_cmd_id` 引用）
- `category` varchar(50)，指令类型（NOTIFY / CHANNEL_CALL / RECONCILE 等）
- `external_order_id` varchar(100)，外部订单 ID（关联业务订单）
- `status` varchar(32)，状态（PENDING / RUNNING / SUCCESS / FAILED）
- `memo` varchar(100)，备注

**时间与版本**
- `created_time` timestamp，创建时间
- `last_updated_time` timestamp，最后更新时间
- `data_version` bigint，数据版本（乐观锁）

## 关联表
| 关联表 | 关系 | 关联键 | 说明 |
|--------|------|--------|------|
| `t_command_param` | 1:N | `t_command_param.id → t_command.id` | 指令执行所需参数 |
| `t_retryable_command` | 1:1 | 同 id | 可重试类指令的扩展属性（重试次数等） |
| `t_unretryable_command` | 1:1 | 同 id | 不可重试类指令的扩展属性 |
| `t_acquire_order` 等订单类表 | N:1 | `xxx_order.current_cmd_id → t_command.id` | 订单当前挂载的指令 |
| `t_stmt_event` / `t_event_param` | 衍生 | 通过 external_order_id | 指令执行后产生的事件 |

## 主键/索引
| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | id | 主键 |
| `i_cmd_eoi` | external_order_id | 按外部订单查指令 |
| `i_urcmd_ct` | created_time | 按时间扫描（调度用） |

## QA 落库检查要点
1. **指令是调度核心**：业务异常常与指令积压相关，排查异步问题先查 `t_command`。
2. **生成验证**：每笔订单创建/状态推进后，应有对应 category 的指令落库，且订单的 `current_cmd_id` 指向该指令。
3. **status 状态机**：PENDING → RUNNING → SUCCESS/FAILED，关注状态流转是否符合预期，避免长时间停留在 RUNNING。
4. **category 决定执行逻辑**：不同 category（NOTIFY / CHANNEL_CALL / RECONCILE 等）走不同处理器，需验证类型与处理逻辑一致。
5. **可重试 vs 不可重试**：通过 `t_retryable_command` / `t_unretryable_command` 区分，需验证指令落入正确的扩展表，且仅有一条扩展记录。
6. **参数完整性**：`t_command_param` 是否包含执行该 category 所需的全部 key（如渠道编号、通知 URL 等）。
7. **积压告警**：PENDING 状态指令若 `created_time` 早于 5 分钟仍未处理，属于调度积压，需告警。
8. **失败排查**：关注 `status = 'FAILED'` 且 `last_updated_time` 在近 1 小时内的指令，可能需重试或人工介入。
9. **乐观锁**：`data_version` 用于并发更新控制，状态变更需校验版本号，避免重复处理。
10. **关联一致性**：`external_order_id` 应能在对应业务订单表中查到，且订单的 `current_cmd_id` 应等于最新一条 t_command.id。