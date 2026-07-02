---
id: tbl_cards_t_import_file
object_type: Table
name: 导入文件 (t_import_file)
aliases: [t_import_file, cards.t_import_file]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cards schema DDL
tags: [card, cards]
sensitivity: normal
related_services: []
---

# 导入文件 (t_import_file)

## 用途
物理表 `cards.t_import_file`,主键 `file_id`。导入文件。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `file_id` | int | 文件id · 可空 |
| `file_type` | char(10) | 文件类型 · 可空 |
| `file_path` | varchar(128) | 文件路径 |
| `status` | char | 文件状态 · 可空 |
| `operator` | varchar(32) | 待补 · 可空 |
| `memo` | varchar(128) | 备注 · 可空 |
| `extension` | varchar(1024) | 扩展参数 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`file_id`
- `uk_import_file_path`:file_path (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
