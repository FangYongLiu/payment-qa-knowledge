---
id: tbl_aml_t_country_config
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
- t_country_config
subdomain: aml
module: null
sensitivity: normal
name: 国家配置表(t_country_config)
aliases:
- t_country_config
related_services:
- svc_aml
related_scenarios: []
---
# 国家配置表(t_country_config)

## 用途
国家配置表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键id |
| `code_alpha2` | char(2) | NOT NULL | 国家code |
| `area_code` | varchar(8) | NOT NULL | 国际编号 |
| `memo` | varchar(64) |  | 备注 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `updated_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
