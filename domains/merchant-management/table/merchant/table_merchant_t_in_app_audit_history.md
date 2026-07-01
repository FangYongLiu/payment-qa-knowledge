---
id: tbl_merchant_t_in_app_audit_history
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
- t_in_app_audit_history
subdomain: merchant
module: null
sensitivity: normal
name: inApp审批历史(t_in_app_audit_history)
aliases:
- t_in_app_audit_history
related_services:
- svc_merchant
related_scenarios: []
---
# inApp审批历史(t_in_app_audit_history)

## 用途
inApp审批历史。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `in_app_order_id` | bigint | NOT NULL | in-app申请订单id |
| `auditor_mid` | varchar(50) | NOT NULL | 审批者会员id |
| `result` | varchar(20) | NOT NULL | 审批结果 PASS  REJECT |
| `comments` | varchar(200) | NOT NULL | 审批意见 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
