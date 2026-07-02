---
id: tbl_acs_t_group_relation
object_type: Table
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (acs schema) 2026-06-25
tags:
- acs
- acs
- t_group_relation
subdomain: acs
module: null
sensitivity: normal
name: 公用关联表(t_group_relation)
aliases:
- t_group_relation
related_services:
- svc_acs
related_scenarios: []
---
# 公用关联表(t_group_relation)

## 用途
公用关联表。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `GROUP_CODE` | varchar(128) | PK / NOT NULL | 组编码 |
| `VALUE_IDENTITY` | varchar(256) | PK / NOT NULL | 值标识 |
| `RELATION_TYPE` | varchar(32) | PK / NOT NULL | 关联类型 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`GROUP_CODE`, `VALUE_IDENTITY`, `RELATION_TYPE`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
