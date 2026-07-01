---
id: tbl_remittance_t_channel_tips
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
- t_channel_tips
subdomain: remittance
module: null
sensitivity: normal
name: 渠道提示信息(t_channel_tips)
aliases:
- t_channel_tips
related_services:
- svc_remittance
related_scenarios: []
---
# 渠道提示信息(t_channel_tips)

## 用途
渠道提示信息。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 启用标识 |
| `channel_code` | varchar(10) | NOT NULL | 渠道代码 |
| `tips_type` | varchar(10) | NOT NULL | 提示类型 |
| `tips_code` | varchar(10) | NOT NULL | 提示code |
| `tips_content` | varchar(255) | NOT NULL | 提示内容 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_type_code` 唯一 (channel_code, tips_type, tips_code)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
