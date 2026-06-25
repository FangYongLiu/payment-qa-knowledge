---
id: tbl_ppcenter_t_gateway_define
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- ppcenter
- pricing
- t_gateway_define
subdomain: pricing
module: null
sensitivity: normal
name: 商户接口组定义(t_gateway_define)
aliases:
- t_gateway_define
related_services:
- svc_ppcenter
related_scenarios: []
---
# 商户接口组定义(t_gateway_define)

## 用途
商户接口组定义。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键id |
| `gateway_group_code` | varchar(64) |  | 接口组code |
| `product_template_id` | int |  | 产品模板id |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | NOT NULL | 修改时间 |
| `gateway_group_name` | varchar(64) |  | 接口组名称 |
| `type` | tinyint(2) |  | 类型 1：产品模板id，2:套餐id |
| `mount_id` | int |  | 类型对应的具体id |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
