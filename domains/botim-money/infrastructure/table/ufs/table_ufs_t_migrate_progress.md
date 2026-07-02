---
id: tbl_ufs_t_migrate_progress
object_type: Table
name: 数据迁移进度表 (t_migrate_progress)
aliases: [t_migrate_progress, ufs.t_migrate_progress]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ufs schema DDL
tags: [infrastructure, ufs]
sensitivity: normal
related_services: []
---

# 数据迁移进度表 (t_migrate_progress)

## 用途
物理表 `ufs.t_migrate_progress`,主键 `id`。数据迁移进度表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | ID · 可空 |
| `bucket` | varchar(50) | Bucket name |
| `progress` | varchar(512) | Progress · 可空 |
| `file_count` | bigint | File Count |
| `status` | char | status: P=迁移中，S=成功, H=暂停 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(512) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- `uk_bucket`:bucket (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
