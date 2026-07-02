---
id: tbl_collection_t_col_change_audit_record
object_type: Table
name: change status audit record (t_col_change_audit_record)
aliases: [t_col_change_audit_record, collection.t_col_change_audit_record]
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

# change status audit record (t_col_change_audit_record)

## 用途
物理表 `collection.t_col_change_audit_record`,主键 `id`。change status audit record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | primay id · 可空 |
| `create_time` | timestamp | create_time · 可空 |
| `create_by` | varchar(64) | create user uid · 可空 |
| `update_time` | timestamp | update_time · 可空 |
| `update_by` | varchar(64) | update user uid · 可空 |
| `biz_no` | varchar(64) | biz no |
| `type` | smallint(4) | type 1:stop |
| `status` | tinyint | -1:fail 0:init 1:success · 可空 |
| `description` | varchar(200) | description · 可空 |
| `file_tags` | varchar(100) | ufs file tag Comma separated · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_biz_no`:biz_no
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
