---
id: tbl_remittance_t_remittance_config
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
- t_remittance_config
subdomain: remittance
module: null
sensitivity: normal
name: 汇款通用配置(t_remittance_config)
aliases:
- t_remittance_config
related_services:
- svc_remittance
related_scenarios: []
---
# 汇款通用配置(t_remittance_config)

## 用途
汇款通用配置。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键ID |
| `partner_id` | varchar(32) | NOT NULL | 平台号;default,payby,botim,totok |
| `channel_code` | varchar(32) | NOT NULL | 渠道code |
| `conf_key` | varchar(45) | NOT NULL | 配置KEY |
| `conf_value` | varchar(255) | NOT NULL | 配置值 |
| `enable_flag` | char | NOT NULL | 是否有效 |
| `memo` | varchar(255) | NOT NULL | 备注 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
