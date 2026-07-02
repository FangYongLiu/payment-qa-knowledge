---
id: tbl_botimcredit_t_cb_credit
object_type: Table
name: 授信表 (t_cb_credit)
aliases: [t_cb_credit, botimcredit.t_cb_credit]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimcredit schema DDL
tags: [lending, botimcredit]
sensitivity: normal
related_services: []
---

# 授信表 (t_cb_credit)

## 用途
物理表 `botimcredit.t_cb_credit`,主键 `id`。授信表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 更新时间 · 可空 |
| `uid` | varchar(45) | 唯一id |
| `status` | int | 状态 |
| `identity` | varchar(128) | 身份证 |
| `finish_time` | timestamp | 完成时间 · 可空 |
| `fee_rate` | smallint unsigned | 费率 |
| `amount` | decimal(15, 2) | 金额 |
| `source` | varchar(20) | 来源 |
| `expire_days` | timestamp | 失效日期 · 可空 |
| `user_id` | varchar(20) | 用户id |
| `type` | smallint | 类型 1授信 2订单 |
| `is_pass_general` | smallint | 是否展示单期 |
| `ext` | varchar(255) | 额外信息 · 可空 |
| `order_no` | varchar(32) | 关联订单号 · 可空 |
| `retry_days_config` | int | retry days config · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_uid`:uid
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
