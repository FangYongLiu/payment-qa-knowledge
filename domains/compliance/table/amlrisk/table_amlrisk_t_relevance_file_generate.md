---
id: tbl_amlrisk_t_relevance_file_generate
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (amlrisk schema) 2026-06-25
tags:
- amlrisk
- amlrisk
- t_relevance_file_generate
subdomain: amlrisk
module: null
sensitivity: normal
name: relevance file generate(t_relevance_file_generate)
aliases:
- t_relevance_file_generate
related_services:
- svc_aml
related_scenarios: []
---
# relevance file generate(t_relevance_file_generate)

## 用途
relevance file generate。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `file_id` | bigint | PK / AUTO_INC | id |
| `param_type` | varchar(32) | NOT NULL | param type: TRADE_ORDER_NO,PAYMENT_ORDER_NO |
| `param_value` | varchar(32) | NOT NULL | param value |
| `file_url` | varchar(200) |  | file url |
| `file_size` | int |  | file size |
| `status` | char | NOT NULL | status: P=processing,F=fail,S=success |
| `error_msg` | varchar(256) |  | error_msg |
| `extension` | varchar(255) |  | Extension |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`file_id`)
- 唯一约束:
  - `uk_paramtype_paramvalue` 唯一 (param_type, param_value)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
