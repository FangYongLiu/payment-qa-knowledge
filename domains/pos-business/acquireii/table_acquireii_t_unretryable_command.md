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
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_command
- tbl_acquireii_t_command_param
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_retryable_command
- tbl_acquireii_t_reversal_order
- tbl_acquireii_t_revoke_order
related_scenarios:
- scn_merchant_transaction_db_check
- scn_mit_autodebit
- scn_mit_cit_directpay_first
- scn_mit_cit_directpay_subsequent
- scn_mit_cit_payandsign
- scn_payby_withdraw_core_cases
- scn_withdraw_to_bank_main_flows
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_unretryable_command`（不可重试指令表）记录**不允许重试**的异步指令。某些指令一旦失败就不能再次执行，因为重复执行会带来资金或状态风险（多扣款、多退款、状态错乱），必须**人工介入**处理。

**典型场景**：
- **支付指令**：重复执行可能导致用户多扣款
- **退款指令**：重复执行可能导致多退款
- **冲正/撤销指令**：重复执行可能导致状态错乱

**与 `t_retryable_command` 的区分**：

| 维度 | t_retryable_command | t_unretryable_command |
|------|---------------------|------------------------|
| 失败处理 | 自动重试（如通知商户、对账） | 不重试，等待人工介入 |
| 资金影响 | 幂等可重入 | 重复执行可能导致资金错乱 |
| 告警优先级 | 一般 | 高优先级 |

表名：`acquireii.t_unretryable_command`，主键 `id`。

## 在交易链路中的位置

收单系统将所有异步动作抽象为「指令(Command)」。主表 `t_command` 承载共性字段，根据指令是否可安全重试，分流到两张子表之一：

```
t_command (1:1)
   ├── t_retryable_command   (可重试：通知、对账等幂等动作)
   └── t_unretryable_command (不可重试：涉及资金的支付/退款/冲正)
t_command_param (1:N)         (指令的入参)
```

当业务流程（如 `t_acquire_order` 触发支付调用、`t_refund_order` 触发退款、`t_revoke_order`/`t_reversal_order` 触发冲正）需要异步执行涉及资金的渠道调用时，会落一条 `t_command` + 一条 `t_unretryable_command`，并在 `t_command_param` 中保存调用参数。一旦失败（status=FAILED），系统不会自动重试，而是进入人工处理流程。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `id` | bigint | ✅ | 主键，对应 `t_command.id`（1:1） |
| `category` | varchar(50) | ✅ | 指令类别（支付/退款/冲正等） |
| `external_order_id` | varchar(100) |  | 外部订单 ID（关联业务订单） |
| `status` | varchar(32) |  | 状态（如 RUNNING、FAILED） |
| `memo` | varchar(100) |  | 备注，常用于记录失败原因 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本（乐观锁） |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `id` | 主键 |
| `i_uc_eoi` | `external_order_id` | 按外部订单查询指令 |
| `i_urcmd_ct` | `created_time` | 按时间扫描（监控/告警） |

## 关联表

| 表 | 关系 | 关联字段 | 说明 |
|----|------|----------|------|
| `t_command` | 1:1 | `id` | 指令主表，承载通用字段 |
| `t_command_param` | 1:N | `id` | 指令参数（调用入参） |
| `t_retryable_command` | 互斥 | `id` | 同一指令二选一，不应共存 |
| `t_acquire_order` / `t_refund_order` / `t_revoke_order` / `t_reversal_order` | 业务关联 | `external_order_id` | 触发指令的业务订单 |

## 校验点（QA 落库检查要点）

1. **失败必须告警**：`status = 'FAILED'` 意味着资金/状态可能错乱，近 1 小时内的失败记录必须被高优先级告警捕获，并产出人工处理工单。
2. **处理中超时检测**：`status = 'RUNNING'` 且 `last_updated_time`（或 `created_time`）超过 5 分钟未更新，可能已卡死，需要排查。
3. **不可随意重置状态**：手动修改 `status`（特别是从 FAILED 改回 RUNNING/INIT）可能导致指令被重复执行，引发多扣款/多退款，禁止运维直接改库。
4. **与重试表互斥**：同一 `id` 应只存在于 `t_retryable_command` 或 `t_unretryable_command` 之一；落库测试时需校验不出现双写。
5. **类别覆盖**：`category` 应覆盖支付调用、退款调用、冲正/撤销调用等所有涉及资金的操作类型；新增涉资金动作时必须落不可重试指令。
6. **与主表一致**：必须存在对应 `t_command` 记录，且 `t_command.category` 与本表 `category` 一致。
7. **参数完整性**：`t_command_param` 中应能查到该指令的完整调用参数，便于人工补单或排查。
8. **data_version 乐观锁**：更新时必须校验 `data_version`，防止并发覆盖导致状态丢失。
9. **external_order_id 可追溯**：通过 `external_order_id` 应能反查到触发该指令的业务订单（支付/退款/冲正/撤销）。
