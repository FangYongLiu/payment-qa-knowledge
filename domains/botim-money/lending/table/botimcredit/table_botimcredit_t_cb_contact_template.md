---
id: tbl_botimcredit_t_cb_contact_template
object_type: Table
name: Contract template table (t_cb_contact_template)
aliases: [t_cb_contact_template, botimcredit.t_cb_contact_template]
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

# Contract template table (t_cb_contact_template)

## 用途
物理表 `botimcredit.t_cb_contact_template`,主键 `id`。Contract template table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Auto-increment ID · 可空 |
| `name` | varchar(128) | Template name |
| `version` | int(64) | Version |
| `html_content` | text | HTML content of the template |
| `create_time` | timestamp | Creation time |
| `file_name` | varchar(128) | File name for user messages, containing placeholders · 可空 |
| `file_size` | int | Size of the PDF file generated from this template · 可空 |

## 主键 / 索引
- 主键:`id`
- `name_version_idx`:name, version (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
