---
id: tbl_statementii_t_statement_config
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
- t_statement_config
subdomain: statement
module: null
sensitivity: normal
name: 对账单配置(t_statement_config)
aliases:
- t_statement_config
related_services:
- svc_statementii
related_scenarios: []
---
# 对账单配置(t_statement_config)

## 用途
对账单配置。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id 主键 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户id |
| `statement_type` | varchar(32) | NOT NULL | 账单类型 FAB_SETTLEMENT FAB_TX |
| `period_type` | varchar(32) | NOT NULL | 期限类型 |
| `start_time` | time |  | 开始时间, 到小时 |
| `last_period_id` | bigint |  | 最后账期id |
| `next_exec_time` | timestamp |  | 下次执行时间 |
| `fail_period_begin_time` | timestamp |  | 失败账期开始时间 |
| `status` | varchar(50) | NOT NULL | 状态  ENABLE 可用 INVALID 无效 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `template_version` | varchar(16) |  | templateVersion |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_mid_stype_ptype` 唯一 (merchant_mid, statement_type, period_type)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
