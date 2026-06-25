---
id: tbl_remittance_t_channel_config
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
- t_channel_config
subdomain: remittance
module: null
sensitivity: normal
name: 渠道配置(t_channel_config)
aliases:
- t_channel_config
related_services:
- svc_remittance
related_scenarios: []
---
# 渠道配置(t_channel_config)

## 用途
渠道配置。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键id |
| `channel_code` | varchar(12) | NOT NULL | 渠道CODE |
| `channel_name` | varchar(100) | NOT NULL | 渠道名称 |
| `country_code` | char(2) |  | 渠道所属国家 |
| `currency` | char(3) |  | 渠道币种 |
| `prefund_currency` | char(3) |  | 预充值币种 |
| `minimum_amount` | decimal(18,6) |  | 最低可用金额 |
| `channel_type` | char(6) | NOT NULL | 渠道类型;direct,common |
| `merchant_id` | varchar(20) |  | 商户号 |
| `merchant_name` | varchar(100) |  | 商户名称 |
| `status` | char | NOT NULL | 状态;N：无效，Y：有效 |
| `extension` | varchar(255) |  | 扩展参数 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
