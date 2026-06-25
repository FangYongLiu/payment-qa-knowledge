---
id: tbl_merchant_t_role
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
- t_role
subdomain: merchant
module: null
sensitivity: normal
name: 角色表(t_role)
aliases:
- t_role
related_services:
- svc_merchant
related_scenarios: []
---
# 角色表(t_role)

## 用途
角色表。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `name` | varchar(32) | NOT NULL | 角色名称 |
| `code` | varchar(32) | NOT NULL | 角色编码 |
| `pcode` | varchar(32) |  | 父级角色编码 |
| `service_provider` | varchar(32) |  | 资源服务提供方，如：MERCHANT,WPS |
| `memo` | varchar(255) |  | 备注 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `UIDX_CODE` 唯一 (code)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
