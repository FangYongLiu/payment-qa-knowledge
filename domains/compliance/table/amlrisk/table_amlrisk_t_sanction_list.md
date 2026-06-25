---
id: tbl_amlrisk_t_sanction_list
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
- t_sanction_list
subdomain: amlrisk
module: null
sensitivity: normal
name: sanction list from focal(t_sanction_list)
aliases:
- t_sanction_list
related_services:
- svc_aml
related_scenarios: []
---
# sanction list from focal(t_sanction_list)

## 用途
sanction list from focal。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | id |
| `sanction_id` | bigint | NOT NULL | id from focal |
| `sanction_code` | varchar(200) | NOT NULL | sanction from focal |
| `short_code` | varchar(200) |  | sanction from focal |
| `create_time` | timestamp(3) | NOT NULL | create_time |
| `update_time` | timestamp(3) | NOT NULL | update_time |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
