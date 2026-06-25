---
id: tbl_merchant_t_paylink_item
object_type: Table
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_paylink_item
subdomain: merchant
module: null
sensitivity: normal
name: paylink_item(t_paylink_item)
aliases:
- t_paylink_item
related_services:
- svc_merchant
related_scenarios: []
---
# paylink_item(t_paylink_item)

## 用途
paylink_item。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `paylink_id` | bigint | NOT NULL | paylink id |
| `name` | varchar(200) | NOT NULL | name |
| `qty` | int | NOT NULL | 份数 |
| `price` | decimal(19,4) | NOT NULL | 单价 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
