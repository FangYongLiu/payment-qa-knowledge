---
id: tbl_escrow_t_clearing_batch
object_type: Table
name: Balance clearing batch table (t_clearing_batch)
aliases: [t_clearing_batch, escrow.t_clearing_batch]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# Balance clearing batch table (t_clearing_batch)

## 用途
物理表 `escrow.t_clearing_batch`,主键 `clearing_batch_id`。Balance clearing batch table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `clearing_batch_id` | bigint | Primary key · 可空 |
| `batch_no` | varchar(64) | Batch number (unique) |
| `bank_code` | char(3) | Bank code: FAB · 可空 |
| `cutoff_time` | timestamp(3) | System cutoff time · 可空 |
| `balance_date` | varchar(10) | FAB file balance snapshot date · 可空 |
| `fab_file_tag` | varchar(255) | FAB balance file UFS fileTag · 可空 |
| `fab_total_cards` | int | FAB file total card count · 可空 |
| `fab_total_balance` | decimal(19, 4) | FAB file total balance · 可空 |
| `sys_total_cards` | int | System total card count · 可空 |
| `sys_total_balance` | decimal(19, 4) | System total balance · 可空 |
| `matched_count` | int | Matched count · 可空 |
| `mismatched_count` | int | Mismatched count · 可空 |
| `fab_only_count` | int | FAB-only count · 可空 |
| `sys_only_count` | int | System-only count · 可空 |
| `diff_amount` | decimal(19, 4) | Net difference (System - FAB) · 可空 |
| `phase` | varchar(4) | Current phase: AL(Alignment)/ZO(Zero-out) · 可空 |
| `align_total` | int | Phase1 total transaction count · 可空 |
| `align_success` | int | Phase1 success count · 可空 |
| `align_failed` | int | Phase1 failed count · 可空 |
| `zero_total` | int | Phase2 total transaction count · 可空 |
| `zero_success` | int | Phase2 success count · 可空 |
| `zero_failed` | int | Phase2 failed count · 可空 |
| `status` | varchar(2) | Batch status: I/SD/RC/CF/RP/PD/AD/ZO/ZR/ZP/CP/CC |
| `operator` | varchar(10) | Operator · 可空 |
| `memo` | varchar(512) | Memo · 可空 |
| `export_file_tag` | varchar(1024) | Export reconciliation result file tag  · 可空 |
| `import_file_tag` | varchar(1024) | Import adjustment file tag  · 可空 |
| `import_txn_count` | int | Import transaction count · 可空 |
| `gmt_create` | timestamp(3) | Created time · 可空 |
| `gmt_modified` | timestamp(3) | Modified time · 可空 |

## 主键 / 索引
- 主键:`clearing_batch_id`
- `uk_batch_no`:batch_no (UNIQUE)
- `idx_clr_bt_gmt_create_status`:gmt_create, status

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
