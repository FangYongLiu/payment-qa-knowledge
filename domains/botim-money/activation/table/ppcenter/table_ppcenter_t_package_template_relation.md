---
id: tbl_ppcenter_t_package_template_relation
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- ppcenter
- pricing
- t_package_template_relation
subdomain: pricing
module: null
sensitivity: normal
name: 产品套餐关系表(t_package_template_relation)
aliases:
- t_package_template_relation
related_services:
- svc_ppcenter
related_scenarios: []
---
# 产品套餐关系表(t_package_template_relation)

## 用途
产品套餐关系表。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键id |
| `template_id` | int(12) | NOT NULL | 模板id |
| `relation_id` | int(12) |  | 产品集 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | NOT NULL | 修改时间 |
| `template_type` | varchar(32) | NOT NULL | 模板类型 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
