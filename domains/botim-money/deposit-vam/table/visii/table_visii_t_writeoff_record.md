---
id: tbl_visii_t_writeoff_record
object_type: Table
name: Write Off Record (t_writeoff_record)
aliases: [t_writeoff_record, visii.t_writeoff_record]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: visii schema DDL
tags: [deposit-vam, visii]
sensitivity: normal
related_services: []
---

# Write Off Record (t_writeoff_record)

## 用途
物理表 `visii.t_writeoff_record`,主键 `writeoff_id`。Write Off Record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `writeoff_id` | bigint | Write Off Record Id |
| `order_id` | bigint | Related Order Id |
| `pre_trade_voucher_no` | varchar(32) | Previous Trade Voucher No · 可空 |
| `writeoff_voucher_no` | varchar(32) | WriteOff Voucher No · 可空 |
| `sub_type` | varchar(16) | Write Off Sub Type: FUNDOUT, REBALANCING, RESET |
| `writeoff_status` | varchar(2) | Write Off Status, I-Initial, PW-Partial WriteOff, FW-Fully WriteOff |
| `amount` | decimal(19, 4) | Amount |
| `currency` | char(3) | Currency, AED |
| `gmt_writeoff` | timestamp(3) | Writeoff time · 可空 |
| `memo` | varchar(128) | Memo · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `gmt_create` | timestamp(3) | Create time |
| `gmt_modified` | timestamp(3) | Modify time · 可空 |

## 主键 / 索引
- 主键:`writeoff_id`
- `uk_writeoff_voucher_no`:writeoff_voucher_no (UNIQUE)
- `idx_writeoff_create`:gmt_create
- `idx_writeoff_order_id`:order_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
