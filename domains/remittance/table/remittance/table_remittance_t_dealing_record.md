---
id: tbl_remittance_t_dealing_record
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
- t_dealing_record
subdomain: remittance
module: null
sensitivity: normal
name: 直连渠道换汇充值记录(t_dealing_record)
aliases:
- t_dealing_record
related_services:
- svc_remittance
related_scenarios: []
---
# 直连渠道换汇充值记录(t_dealing_record)

## 用途
直连渠道换汇充值记录。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `record_id` | bigint | PK / NOT NULL | 主键ID |
| `channel_code` | varchar(12) | NOT NULL | 渠道CODE |
| `country_code` | char(2) | NOT NULL | 国家CODE |
| `value_date_type` | char(4) | NOT NULL | 换汇类型时效;Cash,TOM,SPOT |
| `from_amount` | decimal(15,4) | NOT NULL | 换汇原金额;换汇时的原金额 |
| `from_currency` | char(3) | NOT NULL | 换汇币种;换汇时的币种如USD |
| `to_amount` | decimal(15,4) | NOT NULL | 目标金额;目标金额 |
| `to_currency` | char(3) | NOT NULL | 目标币种;目标币种如PKR |
| `local_amount` | decimal(15,4) | NOT NULL | 本币金额;AED金额 |
| `local_currency` | char(3) | NOT NULL | 本币种;AED |
| `balance_amount` | decimal(18,4) |  | 渠道实时余额 |
| `balance_currency` | char(3) |  | 预存款币种 |
| `base_rate` | decimal(15,8) | NOT NULL | 基础汇率;换汇币种与本币汇率(USD:AED)，保留4位小数 |
| `deal_rate` | decimal(15,8) | NOT NULL | 换汇汇率;换汇币种原币种与目标币种汇率(USD:PKR) |
| `cost_rate` | decimal(15,8) |  | 成本汇率;AED:PKR |
| `status` | char | NOT NULL | 状态;I: Created,V:Valid,C:Cancel |
| `dealing_date` | datetime | NOT NULL | 换汇日期;换汇日期YYYYMMDD |
| `value_date` | datetime |  | 到账日期 |
| `finish_time` | timestamp |  | 完成时间 |
| `operator_name` | varchar(64) |  | 操作员 |
| `operator_time` | timestamp |  | 操作时间 |
| `remark` | varchar(255) |  | 备注;如短信模板需要的变量 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`record_id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
