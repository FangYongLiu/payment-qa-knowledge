---
id: tbl_acquireii_t_command
object_type: Table
domain: acquire-ii-core
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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
收单系统的**异步指令调度核心表**（`acquireii.t_command`），所有需要异步执行的操作都会在此表生成一条指令记录，由调度系统消费执行。所有的发出 id 都从这里读。

典型场景：
- 创建订单后，发出"调用渠道"指令
- 退款后，发出"通知商户"指令
- 定时任务，发出"对账"指令

## 关键列
**主键与指令信息**
- `id` bigint，主键，指令 ID
- `category` varchar(50)，指令类型（NOTIFY / CHANNEL_CALL / RECONCILE 等）
- `external_order_id` varchar(100)，外部订单 ID（关联业务订单）
- `status` varchar(32)，状态（PENDING / RUNNING / SUCCESS / FAILED）
- `memo` varchar(100)，备注

**时间与版本**
- `created_time` timestamp，创建时间
- `last_updated_time` timestamp，最后更新时间
- `data_version` bigint，数据版本（乐观锁）

**关联表**
- `t_command_param` 1:N，通过 id 关联
- `t_retryable_command` 1:1，通过 id 关联
- `t_unretryable_command` 1:1，通过 id 关联
- 各订单类表 N:1，通过 `current_cmd_id → id` 关联

## 主键/索引
| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | id | 主键 |
| `i_cmd_eoi` | external_order_id | 按外部订单查 |
| `i_urcmd_ct` | created_time | 按时间扫描（调度用） |

## 校验点(QA 关注)
1. **指令是调度核心**：业务异常常与指令积压相关，排查异步问题先查 t_command。
2. **status 状态机**：PENDING → RUNNING → SUCCESS/FAILED，关注状态流转是否符合预期。
3. **category 决定执行逻辑**：不同 category 走不同处理器，需验证类型与处理逻辑一致。
4. **可重试 vs 不可重试**：通过 `t_retryable_command` / `t_unretryable_command` 区分，需验证指令落入正确的扩展表。
5. **积压告警**：PENDING 状态指令若 `created_time` 早于 5 分钟仍未处理，属于调度积压，需告警。
6. **失败排查**：关注 `status = 'FAILED'` 且 `last_updated_time` 在近 1 小时内的指令，可能需重试或人工介入。
7. **乐观锁**：`data_version` 用于并发更新控制，状态变更需校验版本号。
