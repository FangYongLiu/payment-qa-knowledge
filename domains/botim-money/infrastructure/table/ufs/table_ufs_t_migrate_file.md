---
id: tbl_ufs_t_migrate_file
object_type: Table
name: 迁移文件 (t_migrate_file)
aliases: [t_migrate_file, ufs.t_migrate_file]
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

# 迁移文件 (t_migrate_file)

## 用途
物理表 `ufs.t_migrate_file`,主键 `id`。迁移文件。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID · 可空 |
| `file_path` | varchar(512) | FilePath · 可空 |
| `bucket` | varchar(50) | Bucket · 可空 |
| `size` | int | Size · 可空 |
| `status` | char | Status: S=Success,E=Exist · 可空 |
| `create_time` | timestamp | Create time |

## 主键 / 索引
- 主键:`id`
- `idx_filepath_bucket`:file_path, bucket

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
