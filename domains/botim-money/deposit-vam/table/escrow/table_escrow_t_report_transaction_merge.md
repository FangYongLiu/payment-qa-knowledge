---
id: tbl_escrow_t_report_transaction_merge
object_type: Table
name: Report Trans Merge (t_report_transaction_merge)
aliases: [t_report_transaction_merge, escrow.t_report_transaction_merge]
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

# Report Trans Merge (t_report_transaction_merge)

## 用途
物理表 `escrow.t_report_transaction_merge`,主键 `merge_id`。Report Trans Merge。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `merge_id` | bigint(32) | Merge Id |
| `fund_id` | varchar(32) | Fund Id |
| `voucher_no` | varchar(32) | Product Order No · 可空 |
| `payment_order_no` | varchar(32) | Debit Order No · 可空 |
| `auth_code` | varchar(6) | Auth Code · 可空 |
| `member_id` | varchar(16) | Member Id · 可空 |
| `card_id` | varchar(18) | Card Id |
| `amount` | decimal(16, 2) | Amount |
| `currency` | char(3) | Currency · 可空 |
| `direction` | varchar(10) | Direction:positive,negetive |
| `report_file_id` | bigint(32) | Report File Id |
| `transaction_num` | int(10) | transaction num |
| `report_category` | varchar(32) | report category · 可空 |
| `transaction_type` | varchar(6) | Transaction Type · 可空 |
| `gmt_fund` | timestamp(6) | Fund Time · 可空 |
| `gmt_create` | timestamp(6) | Create Time |
| `gmt_modified` | timestamp(6) | Modify Time · 可空 |
| `memo` | varchar(64) | Memo · 可空 |
| `extension` | varchar(128) | Extension · 可空 |

## 主键 / 索引
- 主键:`merge_id`
- `uk_trans_merge_card_file`:card_id, report_file_id, direction (UNIQUE)
- `indx_trans_merge_fund_id`:fund_id
- `indx_trans_merge_gmt_fund`:gmt_fund

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
