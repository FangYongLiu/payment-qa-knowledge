---
id: tbl_acquireii_t_revoke_order
object_type: Table
domain: device-pos
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_revoke_order.md
tags:
- 冲正
- revoke
- 收单
subdomain: acquireii
module: null
sensitivity: normal
name: 冲正订单表
aliases:
- t_revoke_order
- acquireii.t_revoke_order
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_reversal_order
- tbl_acquireii_t_reversal_orderii
- tbl_acquireii_t_revoke_order_param
- tbl_acquireii_t_void_ops_order
- tbl_acquireii_t_void_order
related_scenarios:
- scn_merchant_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`t_revoke_order`（冲正订单表）记录收单订单的**冲正（Revoke）**操作及其状态。冲正是一种**异常订单的纠正操作**，常发生在通信超时、系统异常的场景：

- 商户调用接口超时，不知道订单是否已生效
- 商户发起冲正请求，系统帮助确认订单状态
- 如果原订单成功，则冲正成功后状态恢复正常
- 如果原订单失败/不存在，冲正也算成功（防止"幽灵订单"）

### Revoke vs Void vs Reversal（务必区分）

| 语义 | 表 | 说明 |
|------|------|------|
| **Void** | `t_void_order` / `t_void_ops_order` | 商户主动取消订单 |
| **Reversal** | `t_reversal_order` / `t_reversal_orderii` | 系统层面的反向操作（如 ISO 8583 协议层） |
| **Revoke** | `t_revoke_order`（本表） | 上层业务的"冲正"语义，处理通信异常下的状态确认 |

冲正订单本身字段较少，业务参数通过 `t_revoke_order_param` 以 KV 形式扩展关联。

## 在交易链路中的位置

商户发起原支付（落库 `t_acquire_order`）→ 通信/超时异常 → 商户发起 Revoke 请求 → 落库 `t_revoke_order`（主体）+ `t_revoke_order_param`（KV 业务参数） → 系统确认原订单的最终状态 → 回写 `status` / `fail_code` / `fail_message`。

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | 主键，全局号 |
| `status` | varchar(32) |  | 冲正状态 |
| `fail_code` | varchar(50) |  | 错误码 |
| `fail_message` | varchar(200) |  | 错误描述 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本（乐观锁） |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |
| `i_ao_ct` | created_time | 按创建时间范围查询 |

## 关联关系

- **`t_revoke_order_param`**：通过 `global_id` 关联，冲正订单的业务参数 KV 扩展。查询冲正业务详情时通常需要 `LEFT JOIN`。
- **`t_acquire_order`**：原始收单订单主表。冲正操作针对的是该表中的某笔订单，通常通过业务参数（在 `t_revoke_order_param` 中）关联到原订单。
- **同类纠正/取消订单表**：`t_void_order`、`t_void_ops_order`、`t_reversal_order`、`t_reversal_orderii`、`t_refund_order`，配合理解收单链路下不同的取消/纠正语义。

## 校验点（QA 关注）

1. **冲正订单本身字段较少**，业务参数都在 `t_revoke_order_param`，查询时通常需要 LEFT JOIN 取参数。
2. **冲正成功 ≠ 撤销了原订单**，只是确认了原订单的最终状态；如果原订单已成功，冲正后状态恢复正常；如果原订单失败/不存在，冲正也算成功。
3. **冲正失败（`status = 'FAILED'`）需要人工介入**，可能存在资金风险，需关注 `fail_code` / `fail_message`。
4. 近期失败冲正排查参考：`status = 'FAILED' AND created_time >= DATE_SUB(NOW(), INTERVAL 1 DAY)`。
5. 区分 Revoke / Void / Reversal 三种语义，避免混淆：Revoke 处理的是通信异常下的状态确认，而非主动取消（Void）或协议层反向（Reversal）。
6. 落库一致性检查：`t_revoke_order` 与 `t_revoke_order_param` 应同事务写入，`global_id` 必须一致；`last_updated_time` 与 `data_version` 应随状态流转更新。
