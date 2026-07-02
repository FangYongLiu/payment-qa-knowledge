---
id: tbl_collection_col_collection_repay
object_type: Table
name: 还款记录表 (col_collection_repay)
aliases: [col_collection_repay, collection.col_collection_repay]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 还款记录表 (col_collection_repay)

## 用途
物理表 `collection.col_collection_repay`,主键 `id`。还款记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(100) | 更新人员 · 可空 |
| `amount` | decimal(19, 2) | 还款金额 |
| `due_days` | int | 逾期天数 · 可空 |
| `bill_due_days` | smallint(5) | 账单逾期天数 |
| `member_id` | varchar(50) | 债务人id |
| `order_collecton_uid` | varchar(50) | 分案id · 可空 |
| `order_no` | varchar(50) | 订单号 |
| `bill_no` | varchar(64) | 账单号 · 可空 |
| `repay_capital` | decimal(19, 2) | 归还本金 · 可空 |
| `repay_id` | varchar(40) | 还款id |
| `repay_penalty` | decimal(19, 2) | 归还利息 · 可空 |
| `repay_time` | timestamp | 还款时间 |
| `source` | tinyint(5) | 还款渠道 · 可空 |
| `user_uid` | varchar(100) | 催收员 · 可空 |
| `repay_fee` | decimal(19, 2) | 归还手续费 · 可空 |
| `order_source` | smallint(5) | 借款产品码 |
| `type` | tinyint(5) | 还款类型1部分还款 2结清 |
| `extra_content` | varchar(500) | Extra content from repayment MQ, stored as JSON · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_member_id`:member_id
- `idx_order_no`:order_no
- `idx_repay_id`:repay_id
- `idx_repay_time`:repay_time
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
