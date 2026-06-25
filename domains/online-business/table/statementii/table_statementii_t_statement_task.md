---
id: tbl_statementii_t_statement_task
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (statementii schema) 2026-06-25
tags:
- statementii
- statement
- t_statement_task
subdomain: statement
module: null
sensitivity: normal
name: 对账单任务(t_statement_task)
aliases:
- t_statement_task
related_services:
- svc_statementii
related_scenarios: []
---
# 对账单任务(t_statement_task)

## 用途
对账单任务。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id 主键 |
| `statement_config_id` | bigint | NOT NULL | 配置id |
| `settle_config_id` | bigint |  | 结算配置id |
| `statement_id` | bigint |  | 账单id |
| `statement_type` | varchar(32) | NOT NULL | 账单类型 |
| `begin_time` | timestamp | NOT NULL | 开始时间 |
| `end_time` | timestamp | NOT NULL | 结束时间 |
| `status` | varchar(32) | NOT NULL | 状态 CREATED 已创建 STARTED 已开始 STATEMENT_CREATED 对账单已创建 PERIOD_CREATED 账期已创建 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `recon_result` | varchar(32) |  | recon result |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_begin_time` (begin_time)
  - `idx_scid_stype_ctime` (statement_config_id, statement_type, created_time)
  - `idx_st_sci_bt` (statement_config_id, begin_time)
  - `idx_up_stat` (last_updated_time, status)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
