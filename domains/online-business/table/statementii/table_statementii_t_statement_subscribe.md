---
id: tbl_statementii_t_statement_subscribe
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
- t_statement_subscribe
subdomain: statement
module: null
sensitivity: normal
name: 账单订阅(t_statement_subscribe)
aliases:
- t_statement_subscribe
related_services:
- svc_statementii
related_scenarios: []
---
# 账单订阅(t_statement_subscribe)

## 用途
账单订阅。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `config_id` | bigint | NOT NULL | 配置id |
| `merchant_mid` | varchar(50) | NOT NULL | 商户mid |
| `receive_address` | varchar(200) | NOT NULL | 接收地址 |
| `applier_mid` | varchar(50) | NOT NULL | 申请人id |
| `status` | varchar(50) | NOT NULL | 状态 ENABLE 有效；INVALID 无效 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `attach_format` | varchar(10) |  | 附件格式  CSV  XLSX  PDF |
| `PERIOD_TYPE` | varchar(32) |  | 期限类型 DAILY MONTH BOTH |
| `apply_source` | varchar(32) |  | applySource |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
