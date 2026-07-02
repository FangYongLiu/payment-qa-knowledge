---
id: tbl_sqrcredit_t_cs_bill
object_type: Table
name: 帐单信息表 (t_cs_bill)
aliases: [t_cs_bill, sqrcredit.t_cs_bill]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sqrcredit schema DDL
tags: [lending, sqrcredit]
sensitivity: normal
related_services: []
---

# 帐单信息表 (t_cs_bill)

## 用途
物理表 `sqrcredit.t_cs_bill`,主键 `id`。帐单信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `current_status` | smallint(5) | 0 正常还款，未分期，未最低还款 1 最低还款并分期 |
| `amount` | decimal(15, 2) | 金额 |
| `user_id` | varchar(50) | 用户ID |
| `monthly` | smallint(5) | 月份 |
| `check_time` | timestamp | 出帐日期 · 可空 |
| `finish_repay_time` | timestamp | 实际还款时间 · 可空 |
| `due_time` | timestamp | 还款日 · 可空 |
| `bill_no` | varchar(64) | 订单唯一ID |
| `platform` | varchar(20) | 平台 |
| `is_read` | smallint(2) | 状态已读未读 |
| `progress` | smallint(5) | 当前状态 |
| `bill_start_time` | timestamp | 帐单开始时间 · 可空 |
| `bill_end_time` | timestamp | 帐单结束时间 · 可空 |
| `check_amount` | decimal(15, 2) | 出帐金额 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
