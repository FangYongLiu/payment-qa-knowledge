---
id: tbl_remittance_t_delivery_time_stats
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
- t_delivery_time_stats
subdomain: remittance
module: null
sensitivity: normal
name: t_delivery_time_stats
aliases:
- t_delivery_time_stats
related_services:
- svc_remittance
related_scenarios: []
---
# t_delivery_time_stats

## 用途
待补。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | —(DDL未定义) |  |  |
| `channel_code` | —(DDL未定义) |  |  |
| `transaction_mode` | —(DDL未定义) |  |  |
| `to_country_code` | —(DDL未定义) |  |  |
| `to_currency` | —(DDL未定义) |  |  |
| `day_of_week` | —(DDL未定义) |  |  |
| `p50_duration` | —(DDL未定义) |  |  |
| `p75_duration` | —(DDL未定义) |  |  |
| `p90_duration` | —(DDL未定义) |  |  |
| `sample_count` | —(DDL未定义) |  |  |
| `calc_date` | —(DDL未定义) |  |  |
| `create_time` | —(DDL未定义) |  |  |
| `update_time` | —(DDL未定义) |  |  |

## 主键 / 索引
- 主键:(待补)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
