---
id: tbl_aml_t_label_rm_mapping
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_label_rm_mapping
subdomain: aml
module: null
sensitivity: normal
name: 风险等级映射表(t_label_rm_mapping)
aliases:
- t_label_rm_mapping
related_services:
- svc_aml
related_scenarios: []
---
# 风险等级映射表(t_label_rm_mapping)

## 用途
风险等级映射表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键ID |
| `category` | varchar(100) | NOT NULL | 分类 |
| `subcategory` | varchar(150) |  | 分类子类 |
| `risk_level` | tinyint | NOT NULL | 风险等级 |
| `risk_type` | varchar(32) | 默认 '' | 风险类型 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
