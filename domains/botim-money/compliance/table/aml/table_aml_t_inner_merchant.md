---
id: tbl_aml_t_inner_merchant
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
- t_inner_merchant
subdomain: aml
module: null
sensitivity: normal
name: 内部商户表(t_inner_merchant)
aliases:
- t_inner_merchant
related_services:
- svc_aml
related_scenarios: []
---
# 内部商户表(t_inner_merchant)

## 用途
内部商户表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `merchant_id` | varchar(20) | NOT NULL | 商户ID |
| `merchant_name` | varchar(50) |  | 商户名称 |
| `remark` | varchar(50) |  | 备注 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
