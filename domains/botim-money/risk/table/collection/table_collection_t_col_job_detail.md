---
id: tbl_collection_t_col_job_detail
object_type: Table
name: 帐龄分案设置表 (t_col_job_detail)
aliases: [t_col_job_detail, collection.t_col_job_detail]
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

# 帐龄分案设置表 (t_col_job_detail)

## 用途
物理表 `collection.t_col_job_detail`,主键 `id`。帐龄分案设置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `update_by` | varchar(100) | 更新者 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `user_uid` | varchar(100) | 用户id |
| `job_id` | int | 帐龄id |
| `value` | tinyint | 比例值 |
| `enabled` | tinyint | 是否启用 |

## 主键 / 索引
- 主键:`id`
- `idx_job`:job_id
- `idx_user`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
