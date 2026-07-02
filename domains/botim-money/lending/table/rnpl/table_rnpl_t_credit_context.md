---
id: tbl_rnpl_t_credit_context
object_type: Table
name: Context Of Granting Credit Table (t_credit_context)
aliases: [t_credit_context, rnpl.t_credit_context]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Context Of Granting Credit Table (t_credit_context)

## 用途
物理表 `rnpl.t_credit_context`,主键 `id`。Context Of Granting Credit Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | primary Key · 可空 |
| `credit_order_no` | varchar(64) | credit order number |
| `ip` | varchar(30) | 待补 · 可空 |
| `profile_snap` | varchar(10000) | user snapshot |
| `device_snap` | varchar(10000) | device snapshot · 可空 |
| `create_time` | timestamp | create time |

## 主键 / 索引
- 主键:`id`
- `idx_credit_id`:credit_order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
