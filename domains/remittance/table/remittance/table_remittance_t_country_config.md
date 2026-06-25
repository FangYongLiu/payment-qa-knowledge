---
id: tbl_remittance_t_country_config
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
- t_country_config
subdomain: remittance
module: null
sensitivity: normal
name: 国家配置(t_country_config)
aliases:
- t_country_config
related_services:
- svc_remittance
related_scenarios: []
---
# 国家配置(t_country_config)

## 用途
国家配置。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `config_id` | bigint | PK / AUTO_INC | id |
| `country_code` | varchar(10) | NOT NULL | 国家code |
| `code_alpha2` | varchar(10) |  | 两位国家code |
| `enable_flag` | char |  | 启用标识: Y=启用，N=停用 |
| `nationality` | varchar(100) | NOT NULL | 国籍 |
| `default_currency` | varchar(3) | NOT NULL | 默认币种 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |
| `popular_flag` | char |  | 是否主流国家(Y-是，N-否) |
| `area_code` | varchar(8) |  | 国际区号 |

## 主键 / 索引
- 主键:(`config_id`)
- 索引:
  - `uk_nat_def_cur` (nationality, default_currency)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
