---
id: tbl_botimcredit_t_cb_upsell
object_type: Table
name: Easy Cash Upsell Table (t_cb_upsell)
aliases: [t_cb_upsell, botimcredit.t_cb_upsell]
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

# Easy Cash Upsell Table (t_cb_upsell)

## 用途
物理表 `botimcredit.t_cb_upsell`,主键 `id`。Easy Cash Upsell Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | unique id · 可空 |
| `user_id` | varchar(20) | User ID |
| `amount` | decimal(18, 2) | Upsell Loan Amount |
| `created_time` | timestamp | Creation Time |
| `last_modified` | timestamp | Last Modified Time |

## 主键 / 索引
- 主键:`id`
- `uk_user_id`:user_id (UNIQUE)
- `idx_acct_created_time`:created_time
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
