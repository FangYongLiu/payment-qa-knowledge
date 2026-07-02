---
id: tbl_instalment_t_check_file
object_type: Table
name: 对账文件 (t_check_file)
aliases: [t_check_file, instalment.t_check_file]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: instalment schema DDL
tags: [lending, instalment]
sensitivity: normal
related_services: []
---

# 对账文件 (t_check_file)

## 用途
物理表 `instalment.t_check_file`,主键 `file_id`。对账文件。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `file_id` | bigint | 文件id · 可空 |
| `file_type` | varchar(32) | 文件类型：ACCEPT=承兑对账文件 |
| `file_date` | timestamp | 文件日期 |
| `ufs_file_tag` | varchar(50) | UFS文件标签 |
| `create_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`file_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
