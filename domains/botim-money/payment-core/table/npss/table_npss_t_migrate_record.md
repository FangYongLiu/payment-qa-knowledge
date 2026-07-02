---
id: tbl_npss_t_migrate_record
object_type: Table
name: Migrate record table (t_migrate_record)
aliases: [t_migrate_record, npss.t_migrate_record]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# Migrate record table (t_migrate_record)

## 用途
物理表 `npss.t_migrate_record`,主键 `migrate_id`。Migrate record table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `migrate_id` | bigint(19) | Migrate id |
| `migrate_type` | char(2) | Migrate type |
| `ref_id` | varchar(32) | Ref id, unique · 可空 |
| `member_id` | varchar(20) | Member Id · 可空 |
| `old_val` | varchar(32) | Old  val · 可空 |
| `new_val` | varchar(32) | New val · 可空 |
| `status` | char | Migrate Status: I/P/R/S/F |
| `retry_times` | int | Retry times |
| `message` | varchar(128) | Message · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `gmt_create` | timestamp | Create Time |
| `gmt_modified` | timestamp | Modify Time · 可空 |

## 主键 / 索引
- 主键:`migrate_id`
- `uk_migrate_ref`:migrate_type, ref_id (UNIQUE)
- `idx_migrate_modify_time`:gmt_modified

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
