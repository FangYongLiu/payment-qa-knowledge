---
id: tbl_credit_t_cs_early_settlement_info
object_type: Table
name: early settlement info (t_cs_early_settlement_info)
aliases: [t_cs_early_settlement_info, credit.t_cs_early_settlement_info]
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

# early settlement info (t_cs_early_settlement_info)

## 用途
物理表 `credit.t_cs_early_settlement_info`,主键 `id`。early settlement info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `periods` | int | period |
| `user_id` | varchar(32) | user id |
| `interest` | decimal(15, 2) | interest |
| `early_settlement_fee` | decimal(15, 2) | early settlement fee |
| `order_no` | varchar(64) | order no |
| `created_time` | timestamp | created time · 可空 |
| `last_modified` | timestamp | modified time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
