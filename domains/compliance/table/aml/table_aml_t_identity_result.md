---
id: tbl_aml_t_identity_result
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_identity_result
subdomain: aml
module: null
sensitivity: normal
name: 核身结果表(t_identity_result)
aliases:
- t_identity_result
related_services:
- svc_aml
related_scenarios: []
---
# 核身结果表(t_identity_result)

## 用途
核身结果表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `member_id` | varchar(32) | 默认 '' | 会员ID |
| `cis_ticket` | varchar(100) | NOT NULL | 系统生成唯一票据,校验结果时用 |
| `event_type` | varchar(50) | NOT NULL | 事件类型 |
| `inner_out` | varchar(10) |  | 所属内外部-INTERNAL:内部;EXTERNAL:外部 |
| `identity_type` | varchar(64) |  | 核身方式 |
| `sub_identity_type` | varchar(64) |  | 子核身方式 |
| `first_identity_time` | timestamp |  | 第一次验证时间 |
| `result_contant` | varchar(100) | 默认 '' | 结果说明 |
| `checked` | tinyint(2) | 默认 0 | 是否校验过-0.否;1.是; |
| `identity_result` | tinyint(2) | 默认 0 | 核身结果-0.未通过;1.通过; |
| `host_app` | varchar(20) |  | app name |
| `failure_times` | smallint | 默认 0 | 失败次数 |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | 默认 CURRENT_TIMESTAMP | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `cis_ticket` (cis_ticket)
  - `inx_create_time_member_id` (create_time, member_id)
  - `member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
