---
id: tbl_amlrisk_t_transaction_type_mapping
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (amlrisk schema) 2026-06-25
tags:
- amlrisk
- amlrisk
- t_transaction_type_mapping
subdomain: amlrisk
module: null
sensitivity: normal
name: 交易类型映射(t_transaction_type_mapping)
aliases:
- t_transaction_type_mapping
related_services:
- svc_aml
related_scenarios: []
---
# 交易类型映射(t_transaction_type_mapping)

## 用途
交易类型映射。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `biz_product_code` | varchar(10) | PK / NOT NULL | 业务产品码 |
| `transaction_type` | varchar(30) |  | 交易类型 |
| `created_time` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`biz_product_code`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
