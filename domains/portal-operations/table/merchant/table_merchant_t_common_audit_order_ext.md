---
id: tbl_merchant_t_common_audit_order_ext
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
- t_common_audit_order_ext
subdomain: merchant
module: null
sensitivity: normal
name: 审批订单扩展表(t_common_audit_order_ext)
aliases:
- t_common_audit_order_ext
related_services:
- svc_merchant
related_scenarios: []
---
# 审批订单扩展表(t_common_audit_order_ext)

## 用途
审批订单扩展表。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `order_id` | bigint | PK / NOT NULL | 订单ID |
| `pkey` | varchar(200) | PK / NOT NULL | 参数键 |
| `value` | varchar(2000) | NOT NULL | 参数值 |
| `old_value` | varchar(2000) |  | Save old business info of merchant |

## 主键 / 索引
- 主键:(`order_id`, `pkey`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
