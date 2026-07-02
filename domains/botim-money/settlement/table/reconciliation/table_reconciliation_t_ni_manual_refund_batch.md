---
id: tbl_reconciliation_t_ni_manual_refund_batch
object_type: Table
name: NI Manual Refund Batch (t_ni_manual_refund_batch)
aliases: [t_ni_manual_refund_batch, reconciliation.t_ni_manual_refund_batch]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# NI Manual Refund Batch (t_ni_manual_refund_batch)

## 用途
物理表 `reconciliation.t_ni_manual_refund_batch`,主键 `batch_id`。NI Manual Refund Batch。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `batch_id` | bigint | Batch Id: 8 digits date + 9 digits sequence |
| `refund_date` | date | Refund Date |
| `upload_file_tag` | varchar(50) | Upload File Tag |
| `upload_file_name` | varchar(100) | Upload File Name |
| `result_file_tag` | varchar(50) | Result File Tag · 可空 |
| `result_file_name` | varchar(100) | Result File Name · 可空 |
| `count` | int | Count |
| `amount` | decimal(19, 4) | Amount |
| `success_count` | int | Success Count · 可空 |
| `success_amount` | decimal(19, 4) | Success Amount · 可空 |
| `currency` | char(3) | Currency |
| `status` | char | Status: I:Initial U:Uploaded F:Finish |
| `operator` | varchar(32) | Operator |
| `memo` | varchar(255) | Memo · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`batch_id`
- `uk_refund_date`:refund_date (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
