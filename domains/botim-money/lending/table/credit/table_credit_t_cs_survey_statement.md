---
id: tbl_credit_t_cs_survey_statement
object_type: Table
name: Survey Statement (t_cs_survey_statement)
aliases: [t_cs_survey_statement, credit.t_cs_survey_statement]
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

# Survey Statement (t_cs_survey_statement)

## 用途
物理表 `credit.t_cs_survey_statement`,主键 `id`。Survey Statement。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | technical ID · 可空 |
| `statement_id` | char(32) | statement ID |
| `category` | varchar(24) | primary classification |
| `subcategory` | varchar(24) | secondary classification |
| `statement_version` | int | statement version, ascending for new version |
| `scene` | varchar(24) | scene of scene showing |
| `trigger_by` | varchar(32) | survey will be triggered by |
| `survey_attached` | varchar(1024) | attached operations of whole survey |
| `item_sequence` | int | item sequence, zero for TITLE, ascending for other item |
| `item_type` | varchar(8) | item type，TITLE/SINGLE/MULTI/SHORT/BOOL/etc. |
| `item_content` | varchar(255) | item content |
| `item_answer` | varchar(255) | item optional answers |
| `item_attached` | varchar(1024) | attached operations of item |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |
| `version` | int | CAS |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time
- `idx_statementId`:statement_id
- `idx_subcategory`:subcategory

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
