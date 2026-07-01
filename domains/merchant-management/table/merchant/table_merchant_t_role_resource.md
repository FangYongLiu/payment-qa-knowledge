---
id: tbl_merchant_t_role_resource
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
- t_role_resource
subdomain: merchant
module: null
sensitivity: normal
name: 角色与资源关系表(t_role_resource)
aliases:
- t_role_resource
related_services:
- svc_merchant
related_scenarios: []
---
# 角色与资源关系表(t_role_resource)

## 用途
角色与资源关系表。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `role_id` | bigint | NOT NULL | 角色id |
| `resource_id` | bigint | NOT NULL | 资源id |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `UIDX_RID_RSID` 唯一 (role_id, resource_id)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
