---
id: tbl_remittance_t_additional_info_field
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
- t_additional_info_field
subdomain: remittance
module: null
sensitivity: normal
name: 补充信息动态数据配置(t_additional_info_field)
aliases:
- t_additional_info_field
related_services:
- svc_remittance
related_scenarios: []
---
# 补充信息动态数据配置(t_additional_info_field)

## 用途
补充信息动态数据配置。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键id |
| `channel_code` | varchar(12) | NOT NULL | 渠道CODE |
| `field_code` | varchar(32) | NOT NULL | 字段Code |
| `mapping_code` | varchar(50) | NOT NULL | 映射领域对象CODE |
| `show_name` | varchar(64) | NOT NULL | 展示字段名称 |
| `biz_type` | varchar(20) | NOT NULL | 业务类型;Sender，Receiver |
| `additional_type` | varchar(15) |  | 额外信息类型;AML,GW,DL |
| `field_type` | varchar(16) | NOT NULL | 字段类型;如string，date，select |
| `field_max_length` | int |  | 字段值的最大长度 |
| `field_min_length` | int |  | 字段值的最小长度 |
| `field_group` | varchar(32) | NOT NULL | Field分组;标识当前字段所属模块，如kyc信息，职业信息等 |
| `default_value` | varchar(100) |  | 默认值 |
| `validation_regex` | varchar(100) |  | 正则表达式 |
| `hint_msg` | varchar(100) |  | 帮助文案 |
| `tip_msg` | varchar(100) |  | 错误提示文案 |
| `place_holder` | varchar(100) |  | 输入提示 |
| `required_flag` | char | NOT NULL | 是否必填 |
| `sort_no` | int | NOT NULL | 排序号 |
| `transaction_mode` | varchar(30) |  | 汇款方式;bank_transfer,cash_pickup,mobile_wallet |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
