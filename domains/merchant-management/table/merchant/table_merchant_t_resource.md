---
id: tbl_merchant_t_resource
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
- t_resource
subdomain: merchant
module: null
sensitivity: normal
name: 资源(t_resource)
aliases:
- t_resource
related_services:
- svc_merchant
related_scenarios: []
---
# 资源(t_resource)

## 用途
资源。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `name` | varchar(64) | NOT NULL | 资源名称 |
| `code` | varchar(64) | NOT NULL | 资源编码 |
| `pcode` | varchar(64) | NOT NULL | 父级资源编码 |
| `url` | varchar(200) |  | 资源URL |
| `sort` | int |  | 排序 |
| `method` | varchar(32) |  | 请求方式 |
| `service_provider` | varchar(32) |  | 资源服务提供方，如：MERCHANT,WPS |
| `type` | varchar(32) |  | 资源类型，增删改查，预留给WPS做统一接口调用 |
| `resource_group` | varchar(32) |  | Resource Group |
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
