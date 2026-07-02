---
id: tbl_credit_t_cs_activity_applicable_user_whitelist
object_type: Table
name: activity applicable user whitelist table (t_cs_activity_applicable_user_whitelist)
aliases: [t_cs_activity_applicable_user_whitelist, credit.t_cs_activity_applicable_user_whitelist]
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

# activity applicable user whitelist table (t_cs_activity_applicable_user_whitelist)

## 用途
物理表 `credit.t_cs_activity_applicable_user_whitelist`,主键 `id`。activity applicable user whitelist table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | primary key · 可空 |
| `activity_code` | varchar(64) | share code |
| `user_id` | varchar(32) | user id |
| `created_time` | timestamp | created time |

## 主键 / 索引
- 主键:`id`
- `idx_user_id_activity_code`:user_id, activity_code

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
