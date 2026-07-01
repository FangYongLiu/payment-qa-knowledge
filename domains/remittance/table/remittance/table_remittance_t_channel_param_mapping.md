---
id: tbl_remittance_t_channel_param_mapping
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
- t_channel_param_mapping
subdomain: remittance
module: null
sensitivity: normal
name: 渠道参数值映射(t_channel_param_mapping)
aliases:
- t_channel_param_mapping
related_services:
- svc_remittance
related_scenarios: []
---
# 渠道参数值映射(t_channel_param_mapping)

## 用途
渠道参数值映射。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键ID |
| `channel_code` | varchar(32) |  | 渠道CODE |
| `param_key` | varchar(32) | NOT NULL | 参数KEY |
| `param_value` | varchar(32) | NOT NULL | 参数值 |
| `mapping_value` | varchar(120) | NOT NULL | Mapping value |
| `mapping_label` | varchar(100) |  | 渠道映射显示值 |
| `filter_info` | varchar(100) |  | 过滤条件 |
| `output_info` | varchar(100) |  | 输出 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
