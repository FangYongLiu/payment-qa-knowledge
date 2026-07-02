---
id: tbl_remittance_t_field_mapping
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
- t_field_mapping
subdomain: remittance
module: null
sensitivity: normal
name: 字段映射表(t_field_mapping)
aliases:
- t_field_mapping
related_services:
- svc_remittance
related_scenarios: []
---
# 字段映射表(t_field_mapping)

## 用途
字段映射表。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC |  |
| `channel_code` | varchar(10) | NOT NULL | 渠道code |
| `channel_field` | varchar(50) | NOT NULL | 渠道字段 |
| `field_code` | varchar(32) | NOT NULL | 字段code |
| `show_name` | varchar(50) | NOT NULL | 展示字段 |
| `update_time` | timestamp | NOT NULL | 修改时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_cc_cf` 唯一 (channel_code, channel_field)
  - `uk_cc_fc` 唯一 (channel_code, field_code)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
