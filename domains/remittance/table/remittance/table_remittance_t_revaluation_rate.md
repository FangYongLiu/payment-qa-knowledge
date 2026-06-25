---
id: tbl_remittance_t_revaluation_rate
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
- t_revaluation_rate
subdomain: remittance
module: null
sensitivity: normal
name: 直连渠道预估汇率(t_revaluation_rate)
aliases:
- t_revaluation_rate
related_services:
- svc_remittance
related_scenarios: []
---
# 直连渠道预估汇率(t_revaluation_rate)

## 用途
直连渠道预估汇率。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `channel_code` | varchar(12) | NOT NULL | 渠道CODE |
| `country_code` | char(2) | NOT NULL | 国家CODE |
| `transaction_mode` | varchar(16) | NOT NULL | 汇款模式 |
| `currency` | char(3) | NOT NULL | 余额币种;币种如PKR |
| `revaluation_rate` | decimal(15,8) | NOT NULL | 估值汇率 |
| `status` | char | NOT NULL | 状态;I:Invalid,V:Valid |
| `operator_name` | varchar(64) |  | 操作员 |
| `operator_time` | timestamp |  | 操作时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
