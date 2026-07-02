---
id: tbl_remittance_t_dynamic_field
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
- t_dynamic_field
subdomain: remittance
module: null
sensitivity: normal
name: 字段映射表(t_dynamic_field)
aliases:
- t_dynamic_field
related_services:
- svc_remittance
related_scenarios: []
---
# 字段映射表(t_dynamic_field)

## 用途
字段映射表。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键id |
| `channel_code` | varchar(32) | NOT NULL | 渠道CODE |
| `field_code` | varchar(32) | NOT NULL | 字段Code |
| `mapping_code` | varchar(32) |  | 映射实体类的匹配code |
| `show_name` | varchar(64) |  | 展示字段名称 |
| `biz_type` | varchar(32) | NOT NULL | 业务类型;Sender，Receiver |
| `field_type` | varchar(12) | NOT NULL | 字段类型;如string，date，select |
| `field_max_length` | int |  | 字段值的最大长度 |
| `field_min_length` | int |  | 字段值的最小长度 |
| `field_max_value` | int |  | 最大值限制 |
| `field_min_value` | int |  | 最小值限制 |
| `field_group` | varchar(32) |  | Field分组;标识当前字段所属模块，如kyc信息，职业信息等 |
| `group_name` | varchar(100) |  | 组名称;用于前端分组时展示 |
| `default_value` | varchar(100) |  | 默认值 |
| `validation_regex` | varchar(128) |  | 内容正则校验 |
| `hint_msg` | varchar(128) |  | 输入框提示内容文案 |
| `tip_msg` | varchar(128) |  | 错误提示内容文案 |
| `level` | int |  | Sender等级;如cdd0,cdd1,cdd2,不同等级需要的参数不同，99代表默认收集的 |
| `country_code` | varchar(6) |  | 3位国家CODE |
| `transaction_mode` | varchar(32) |  | 服务类型;banktransfer,pickup |
| `currency` | char(3) |  | 币种;受益人收款币种 |
| `required_flag` | char | NOT NULL | 是否必填 |
| `sort_no` | int |  | 排序号 |
| `upper_key` | varchar(32) |  | 上级field |
| `relation_key` | varchar(32) |  | 下级field |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
