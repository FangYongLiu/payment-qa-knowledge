---
id: tbl_fiserv_refund_bucket
object_type: Table
domain: channel-integration
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_fiserv_refund_bucket.md
tags:
- refund
- bucket
- fiserv
subdomain: refund
module: null
sensitivity: normal
name: Fiserv退款资金桶表
aliases:
- t_fiserv_refund_bucket
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

记录一笔 Fiserv 订单的**退款额度池**，管理三态金额：可退款金额（refundable）、退款中金额（refunding）、已退款金额（refunded）。

表名：`acquireii.t_fiserv_refund_bucket`，主键 `global_id`，对应订单 global_id。

**典型流转**（以 1000 订单为例）：
- 初始：refundable=1000, refunding=0, refunded=0
- 发起退款 300：refunding=300, refundable=700
- 退款成功：refunded=300, refunding=0, refundable=700
- 再退 200：refunded=500, refundable=500
- 退款失败：refunding → refundable 回退

## 关键列

### 主键
- `global_id` bigint：主键，对应订单 global_id

### 可退款金额（剩余可退）
- `refundable_currency_code` varchar(50)
- `refundable_amount` decimal(19,4)：还能退多少

### 退款中金额（处理中）
- `refunding_currency_code` varchar(50)
- `refunding_amount` decimal(19,4)

### 已退款金额（已成功）
- `refunded_currency_code` varchar(50)
- `refunded_amount` decimal(19,4)

### 时间与版本
- `created_time` timestamp(3)
- `last_updated_time` timestamp(3)
- `data_version` bigint：乐观锁版本号

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |
| `i_frb_ct` | created_time | 按创建时间查询 |
| `i_frb_lut` | last_updated_time | 按更新时间查询 |

**关联关系**：
- 1:1 → `t_fiserv_sale_order`（global_id）
- 1:N → `t_fiserv_refund_order`（origin_global_id → global_id）

## 校验点(QA 关注)

1. **三态金额平衡**：`refundable_amount + refunding_amount + refunded_amount = 原订单金额`，误差应 < 0.01。可用 JOIN `t_fiserv_sale_order` 校验。
2. **乐观锁**：更新必须带 `data_version`，并发场景下防止覆盖。
3. **退款失败回退**：退款失败时 `refunding_amount` 必须回退到 `refundable_amount`，不可残留在 refunding 态。
4. **多次退款共用 bucket**：同一 global_id 的 bucket 唯一，多次退款通过 `t_fiserv_refund_order.origin_global_id` 关联，bucket 只增量更新。
5. **净可退计算**：实际可发起退款金额 = `refundable_amount - refunding_amount`，避免重复发起超额退款。
6. **币种一致性**：refundable/refunding/refunded 三个 currency_code 应与原订单币种一致。
