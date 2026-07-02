---
id: tbl_credit_t_cs_direct_debit_mandate
object_type: Table
name: order direct debit mandates table (t_cs_direct_debit_mandate)
aliases: [t_cs_direct_debit_mandate, credit.t_cs_direct_debit_mandate]
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

# order direct debit mandates table (t_cs_direct_debit_mandate)

## 用途
物理表 `credit.t_cs_direct_debit_mandate`,主键 `id`。order direct debit mandates table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | id · 可空 |
| `user_id` | varchar(20) | user ID |
| `order_no` | varchar(64) | order no |
| `mandate` | text | mandate · 可空 |
| `latest_mandate_status` | varchar(16) | latest mandate status · 可空 |
| `updated_time` | timestamp | update time · 可空 |
| `created_time` | timestamp | created time |
| `ddar_id` | varchar(64) | ddar_id · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time
- `idx_ddar_id`:ddar_id
- `idx_order_no`:order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
