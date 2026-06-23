---
id: tbl_pos_settlement
object_type: Table
domain: device-pos
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_pos_settlement.md
tags:
- pos
- settlement
- 结算
subdomain: settlement
module: null
sensitivity: normal
name: POS结算表
aliases:
- t_pos_settlement
- acquireii.t_pos_settlement
related_services: []
related_tables:
- tbl_fiserv_batch
- tbl_fiserv_refund_order
- tbl_fiserv_reversal_order
- tbl_fiserv_sale_order
- tbl_fiserv_sale_void_ops_order
- tbl_hardware_info
- tbl_merchant_device
- tbl_pos_settlement_history
related_scenarios:
- scn_fiserv_test_tid_creation
- scn_payment_code_scanned_by_pos
- scn_payment_code_scanned_by_scanner
- scn_pos_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`t_pos_settlement` 记录 POS 设备的**活跃结算操作**（日终结算 / 批结算）。POS 每天打烊时由收银员发起结算，系统统计当天交易、与 Fiserv / 卡组织对账，结算完成后才能产生最终的 Settlement Report。

本表只保存**进行中/活跃**的结算记录；结算完成后记录会被移至 `tbl_pos_settlement_history`，因此本表不应残留已完成结算。

典型场景：
- 收银员每天打烊前在 POS 上点"结算"
- 系统按设备维度统计当天交易（`t_acquire_order` 等）并与 Fiserv 批次对账
- 结算完成 → 移入历史表 → 生成 Settlement Report

## 在交易链路中的位置

```
刷卡交易（Fiserv Sale/Void/Refund/Reversal Order）
        ↓ 按 device_id + created_time 归集
  t_pos_settlement（活跃，本表）  ← 收银员触发日终结算
        ↓ 结算完成 / 对账成功
  t_pos_settlement_history（已完成）
        ↓
  Settlement Report 生成 / Fiserv 批次（t_fiserv_batch）落地
```

## 关键列

| 字段 | 类型 | 说明 |
|------|------|------|
| `settlement_id` | bigint | 主键，结算 ID |
| `device_id` | varchar(32) | 设备 ID（唯一约束，活跃期间唯一） |
| `partner_id` | varchar(32) | 商户 ID |
| `start_time` | timestamp(3) | 结算开始时间（结算窗左边界） |
| `end_time` | timestamp(3) | 结算结束时间（结算窗右边界） |
| `operator_id` | varchar(50) | 操作员 ID（执行结算的收银员，用于审计） |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本（乐观锁） |

所有字段均必填。

## 主键 / 索引

- **PRIMARY**：`settlement_id`
- **`uk_ps_device`**：`device_id` —— 唯一约束，**同一设备同时只能有一条活跃结算**
- **`i_ps_lut`**：`last_updated_time` —— 按更新时间查询/扫描

## 与关联表的关系

| 关联表 | 关联键 | 关系说明 |
|--------|--------|----------|
| `tbl_pos_settlement_history` | `settlement_id` / `device_id` | 结算完成后记录从本表迁移至历史表 |
| `tbl_merchant_device` | `device_id` + `partner_id` | 校验设备与商户归属一致性 |
| `tbl_hardware_info` | `device_id` | 设备基础信息 |
| `tbl_fiserv_sale_order` / `tbl_fiserv_sale_void_ops_order` / `tbl_fiserv_refund_order` / `tbl_fiserv_reversal_order` | `device_id` + `created_time ∈ [start_time, end_time]` | 结算窗内的交易订单需被纳入本次结算 |
| `tbl_fiserv_batch` | 结算触发批次 | 结算完成后形成 Fiserv 批次，进入清算对账 |
| `t_acquire_order` | `device_id` + `created_time BETWEEN start_time AND end_time` | 收单订单按结算窗归集 |

## 校验点（QA 关注）

1. **device_id 唯一约束**：同一设备同一时刻只能存在一条活跃结算记录，重复插入必须被 `uk_ps_device` 拒绝。
2. **活跃 vs 历史分离**：结算完成后记录应从 `t_pos_settlement` 移至 `t_pos_settlement_history`，本表不应残留已完成结算；QA 校验时需联查两表。
3. **结算时间窗 `[start_time, end_time]`**：用于关联 `t_acquire_order` 与 Fiserv 各订单表（`device_id` + `created_time BETWEEN start_time AND end_time`），需校验：
   - `end_time >= start_time`
   - 同一设备相邻结算窗连续、不重叠、不留空隙
4. **结算维度**：必须按设备（`device_id`）维度执行，跨设备需分别结算，不允许一条记录覆盖多设备。
5. **operator_id 审计**：必须记录执行结算的收银员，不可为空，便于追溯。
6. **partner_id 一致性**：本表的 `partner_id` 必须与 `tbl_merchant_device` 中 `device_id` 所属商户一致。
7. **data_version 并发控制**：更新时基于 `data_version` 做乐观锁控制，避免并发结算覆盖。
8. **落库检查典型查询**：
   ```sql
   -- 查活跃结算
   SELECT * FROM t_pos_settlement WHERE device_id = ?;
   -- 查结算窗内的交易
   SELECT * FROM t_fiserv_sale_order
   WHERE device_id = ?
     AND created_time BETWEEN ? AND ?;
   ```
