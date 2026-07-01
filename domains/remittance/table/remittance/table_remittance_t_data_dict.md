---
id: tbl_remittance_t_data_dict
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
- t_data_dict
subdomain: remittance
module: null
sensitivity: normal
name: 数字字典配置表(t_data_dict)
aliases:
- t_data_dict
related_services:
- svc_remittance
related_scenarios: []
---
# 数字字典配置表(t_data_dict)

## 用途
数字字典配置表。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `group_code` | varchar(32) | NOT NULL | 分组code |
| `group_name` | varchar(64) | NOT NULL | 分组名字 |
| `data_key` | varchar(32) | NOT NULL | 数据key |
| `data_value` | varchar(255) | NOT NULL | 数据值 |
| `memo` | varchar(255) |  | 备注 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
