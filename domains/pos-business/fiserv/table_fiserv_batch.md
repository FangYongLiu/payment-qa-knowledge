---
id: tbl_fiserv_batch
object_type: Table
domain: device-pos
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_fiserv_batch.md
tags:
- fiserv
- 批次
- 收单
subdomain: fiserv
module: batch
sensitivity: normal
name: Fiserv批次表
aliases:
- t_fiserv_batch
- acquireii.t_fiserv_batch
related_services: []
related_tables:
- tbl_fiserv_refund_order
- tbl_fiserv_reversal_order
- tbl_fiserv_sale_order
- tbl_fiserv_sale_void_ops_order
- tbl_hardware_info
- tbl_merchant_device
- tbl_pos_settlement
related_scenarios:
- scn_fiserv_test_tid_creation
- scn_merchant_transaction_db_check
- scn_pos_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_fiserv_batch` 是 Fiserv 国际收单渠道的**批次管理表**，按设备维度组织结算批次。Fiserv 采用批次结算模式：每个 POS 设备在一段时间内的交易组成一个批次（Batch），批次结束后统一上送 Fiserv 进行清算。

典型场景：
- POS 设备每天打烊时做一次批次结算（Settlement / Batch Close）
- 批次内所有交易（sale / refund / void / reversal）一起对账
- 一个 `device_id` 同时只能有一个开放（活跃）批次

## 在交易链路中的位置

```
设备激活 (tbl_active_code / tbl_hardware_info / tbl_merchant_device)
        │
        ▼
  打开批次 → t_fiserv_batch (本表，按 device_id 唯一)
        │
        ├── 销售   → tbl_fiserv_sale_order
        ├── 退款   → tbl_fiserv_refund_order
        ├── 撤销   → tbl_fiserv_sale_void_ops_order
        └── 冲正   → tbl_fiserv_reversal_order
        │
        ▼
  关闭批次 (end_time 落地) → 上送 Fiserv 清算
        │
        ▼
  POS 结算: tbl_pos_settlement / tbl_pos_settlement_history
```

本表是 Fiserv 渠道交易归集的**锚点**：所有 Fiserv 交易明细通过 `device_id` + 交易时间区间 与该表绑定，批次关闭后驱动下游结算。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `batch_id` | bigint | ✅ | 主键，批次 ID |
| `device_id` | varchar(32) | ✅ | 设备 ID（唯一约束，关联 `tbl_merchant_device` / `tbl_hardware_info`） |
| `partner_id` | varchar(32) | ✅ | 商户 ID |
| `start_time` | timestamp(3) | ✅ | 批次开始时间 |
| `end_time` | timestamp(3) | ✅ | 批次结束时间 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本（乐观锁） |

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `batch_id` | 主键 |
| `uk_fb_device` | `device_id` | 唯一约束（一个设备一个活跃批次） |
| `i_fb_lut` | `last_updated_time` | 按更新时间查询/增量同步 |

## 与关联表的关系

| 关联表 | 关联字段 | 关系说明 |
|--------|----------|----------|
| `tbl_fiserv_sale_order` | `device_id` + `created_time ∈ [start_time, end_time]` | 批次内销售交易 |
| `tbl_fiserv_refund_order` | 同上 | 批次内退款交易 |
| `tbl_fiserv_sale_void_ops_order` | 同上 | 批次内撤销操作 |
| `tbl_fiserv_reversal_order` | 同上 | 批次内冲正交易 |
| `tbl_merchant_device` | `device_id` | 设备所属商户 |
| `tbl_hardware_info` | `device_id` | 设备硬件信息 |
| `tbl_pos_settlement` / `tbl_pos_settlement_history` | 批次关闭后驱动结算 | 下游清算 |

## QA 落库检查要点

1. **device_id 唯一约束**：一个设备同时只能存在一个活跃批次，重复创建应被 `uk_fb_device` 拒绝。
2. **批次范围**：批次内交易由 `device_id` + 时间区间确定，关联 SQL 形如：
   ```sql
   SELECT s.*
   FROM t_fiserv_sale_order s
   JOIN t_fiserv_batch b ON s.device_id = b.device_id
   WHERE s.created_time BETWEEN b.start_time AND b.end_time;
   ```
3. **批次关闭后不可再加入交易**：`end_time` 落地后新交易不应再归属于该批次，需新开批次。
4. **查询设备当前批次**：
   ```sql
   SELECT * FROM t_fiserv_batch WHERE device_id = ?;
   ```
5. **时间一致性**：`start_time ≤ end_time`、`created_time ≤ last_updated_time`，且批次内每笔交易的 `created_time` 必须在区间内。
6. **data_version**：批次状态更新（如关闭批次）应通过乐观锁递增，验证并发场景下不会出现脏写。
7. **构造测试 TID/批次**：参考 `scn_fiserv_test_tid_creation` 在测试环境创建 device 与初始批次。
8. **跨表对账**：`tbl_fiserv_sale_order` 等明细的 `device_id` 必须能在本表找到匹配批次记录，否则视为孤儿交易。
