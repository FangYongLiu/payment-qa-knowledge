---
id: tbl_remittance_t_currency_blacklist
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
- t_currency_blacklist
subdomain: remittance
module: null
sensitivity: normal
name: 币种黑名单(t_currency_blacklist)
aliases:
- t_currency_blacklist
related_services:
- svc_remittance
related_scenarios: []
---
# 币种黑名单(t_currency_blacklist)

## 用途
币种黑名单。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `config_id` | bigint | PK / AUTO_INC | 配置id |
| `currency_code` | varchar(3) | NOT NULL | 币种: ALL=全匹配 |
| `inst_code` | varchar(32) |  | 机构code |
| `country_code` | varchar(32) | NOT NULL | 国家code: ALL=全匹配 |
| `enable_flag` | char | NOT NULL | 启用标识: Y=启用，N=停用 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`config_id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
