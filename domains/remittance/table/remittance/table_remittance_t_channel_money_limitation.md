---
id: tbl_remittance_t_channel_money_limitation
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
- t_channel_money_limitation
subdomain: remittance
module: null
sensitivity: normal
name: 渠道限额表(t_channel_money_limitation)
aliases:
- t_channel_money_limitation
related_services:
- svc_remittance
related_scenarios: []
---
# 渠道限额表(t_channel_money_limitation)

## 用途
渠道限额表。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id: 主键 |
| `channel_code` | varchar(32) | NOT NULL | 渠道编码 |
| `transaction_mode` | varchar(20) | NOT NULL | 汇款模式 |
| `to_country` | char(3) | NOT NULL | 目标国家 |
| `to_currency` | char(3) | NOT NULL | 目标币种 |
| `single_max_value` | decimal(19,4) | NOT NULL | 限额值 |
| `status` | char | NOT NULL | 状态:Y-有效，N-无效 |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
