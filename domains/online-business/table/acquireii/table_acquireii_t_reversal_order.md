---
id: tbl_acquireii_t_reversal_order
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_reversal_order.md
tags:
- reversal
- 协议层
- 订单表
subdomain: acquireii
module: reversal
sensitivity: normal
name: Reversal订单表
aliases:
- acquireii.t_reversal_order
related_services:
- svc_acquireii
---

## 用途

`acquireii.t_reversal_order` 用于记录 **reversal**（协议层反向冲账）订单。

- **Reversal**：支付协议层（如 ISO 8583）的反向操作，用于纠正原订单的资金流向。
- 与 **Revoke（冲正，业务层语义，落库于 `t_revoke_order` / `t_revoke_order_param`）** 区分：reversal 处理的是"协议层异常时的反向报文"。
- 典型场景：交易已下发到卡组织，但应答异常（超时、网络中断、报文不一致等），系统自动发起 reversal 报文，由卡组织根据该报文回滚资金。
- 通常由系统自动触发，**非商户主动调用**。
- 新订单已迁移至升级版表 `t_reversal_orderii`，本表只保留存量数据。

## 在交易链路中的位置

```
t_acquire_order (主订单, 协议层异常)
      │
      ▼
 t_command (调度反向指令)
      │
      ▼
 t_reversal_order  ←—— 本表（存量）
      │
      ▼
 t_reversal_orderii ←—— 新订单走这里
```

- 上游：`t_acquire_order` 主订单在协议层异常时触发 reversal。
- 调度：通过 `t_command` 系列（含 `t_retryable_command` / `t_unretryable_command`）下发反向报文。
- 兄弟语义：
  - `t_revoke_order` = 业务层冲正
  - `t_void_order` = 撤销
  - `t_refund_order` = 退款
  - `t_reversal_order(ii)` = 协议层反向冲账（本表所属）

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `global_id` | bigint | ✅ | 主键，全局号，可关联主订单 / 指令系统 |
| `status` | varchar(32) |  | reversal 状态（如 `FAILED`） |
| `fail_code` | varchar(50) |  | 错误码 |
| `fail_message` | varchar(200) |  | 错误描述 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本（乐观锁） |

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_ao_ct` | `created_time` | 按时间查询 |

## 关联关系

| 关联表 | 关联字段 | 说明 |
|--------|----------|------|
| `t_acquire_order` | `global_id` | 关联原始收单订单 |
| `t_command` / `t_retryable_command` / `t_unretryable_command` | `global_id` | 关联协议层指令调度记录 |
| `t_reversal_orderii` | `global_id` | 升级版表，新订单写入此表 |
| `t_revoke_order` | 业务语义对照 | 区分协议层 vs 业务层冲正 |

## QA 落库检查要点

1. **Reversal 失败有资金风险**：`status = 'FAILED'` 意味着资金已划走但回滚失败，需重点排查并核对账务。
2. 关注 `fail_code` / `fail_message`：定位协议层异常原因（超时、报文不匹配、卡组织拒绝等）。
3. 区分 reversal（协议层） vs revoke（业务层冲正），不要混淆语义；查询时确认查的是 `t_reversal_order(ii)` 还是 `t_revoke_order`。
4. Reversal 通常由系统自动触发，若出现异常调用来源（人工触发、商户接口）需告警。
5. 新订单已迁移至 `t_reversal_orderii`，本表关注存量；如新订单未在 ii 表落库，需排查路由是否正确。
6. 通过 `global_id` 反查 `t_acquire_order` 与 `t_command`，确认主订单状态与指令重试链路是否闭环。

## 常用排查 SQL

```sql
-- 近 1 天 reversal
SELECT * FROM t_reversal_order
WHERE created_time >= DATE_SUB(NOW(), INTERVAL 1 DAY);

-- 失败 reversal（资金风险点）
SELECT * FROM t_reversal_order
WHERE status = 'FAILED'
ORDER BY created_time DESC;
```
