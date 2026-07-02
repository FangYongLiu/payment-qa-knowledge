---
id: tbl_merchant_t_merchant_status_history
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_merchant_status_history
subdomain: merchant
module: null
sensitivity: normal
name: Merchant Status History table(t_merchant_status_history)
aliases:
- t_merchant_status_history
related_services:
- svc_merchant
related_scenarios: []
---
# Merchant Status History table(t_merchant_status_history)

## 用途
Merchant Status History table。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | ID |
| `merchant_mid` | varchar(32) | NOT NULL | Merchant Mid |
| `merchant_status` | varchar(32) | NOT NULL | Merchant Status |
| `reason_type` | varchar(32) |  | Reason TYPE |
| `specific_reason` | varchar(255) |  | Specific Reason |
| `description` | varchar(255) |  | description |
| `operator_id` | varchar(32) | NOT NULL | Operator ID |
| `operator_name` | varchar(128) | NOT NULL | Operator Name |
| `created_time` | timestamp |  | Created time |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
