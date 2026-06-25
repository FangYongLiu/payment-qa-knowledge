---
id: tbl_remittance_t_exchange_rate_statistics
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_exchange_rate_statistics
subdomain: remittance
module: null
sensitivity: normal
name: 汇率统计表(t_exchange_rate_statistics)
aliases:
- t_exchange_rate_statistics
related_services:
- svc_remittance
related_scenarios: []
---
# 汇率统计表(t_exchange_rate_statistics)

## 用途
汇率统计表。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `statistics_type` | varchar(12) |  | 统计类型，近7天（DAYS），近1个月(MONTH)，近半年（HALF_YEAR) |
| `from_country_code` | char(2) | NOT NULL | 国家code |
| `from_currency` | char(3) | NOT NULL | 币种 |
| `to_country_code` | char(2) | NOT NULL | 目标国家code |
| `to_currency` | char(3) | NOT NULL | 目标国家币种 |
| `transaction_mode` | varchar(32) | NOT NULL | 汇款模式 |
| `current_rate` | decimal(15,8) | NOT NULL | 当前汇率 |
| `maximum_rate` | decimal(15,8) | NOT NULL | 最高汇率 |
| `minimum_rate` | decimal(15,8) | NOT NULL | 最低汇率 |
| `start_time` | datetime |  | 统计开始日期 |
| `end_time` | datetime |  | 统计结束日期 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
