---
id: tbl_credit_t_cs_limit_log
object_type: Table
name: record limit changelog (t_cs_limit_log)
aliases: [t_cs_limit_log, credit.t_cs_limit_log]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# record limit changelog (t_cs_limit_log)

## 用途
物理表 `credit.t_cs_limit_log`,主键 `id`。record limit changelog。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | key · 可空 |
| `user_id` | varchar(20) | 用户id |
| `created_type` | varchar(20) | settle/overdue/display/email/operator/lean_tech/display_rule · 可空 |
| `limit_type` | varchar(20) | credit_amount/temporary_amount/display_amount · 可空 |
| `before_limit` | decimal(15, 2) | before limit · 可空 |
| `after_limit` | decimal(15, 2) | after limit · 可空 |
| `changed_temp_amt` | decimal(15, 2) | change temp amount · 可空 |
| `before_temp_amt` | decimal(15, 2) | after temp amount · 可空 |
| `after_temp_amt` | decimal(15, 2) | after temp amount · 可空 |
| `changed_amount` | decimal(15, 2) | limit · 可空 |
| `product` | varchar(20) | small/payonce/2 months/3 months/6 months/pro_loan · 可空 |
| `last_order_overdue_days` | varchar(20) | last_settled_order overdue days (early settlement will be negative number) · 可空 |
| `last_settled_order` | varchar(64) | setted order · 可空 |
| `ext` | varchar(255) | ext · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
