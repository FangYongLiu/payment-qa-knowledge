---
id: tbl_ppcenter_t_advance_define
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
- t_advance_define
subdomain: pricing
module: null
sensitivity: normal
name: 高级属性配置表(t_advance_define)
aliases:
- t_advance_define
related_services:
- svc_ppcenter
related_scenarios: []
---
# 高级属性配置表(t_advance_define)

## 用途
高级属性配置表。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | ID |
| `ad_type` | varchar(25) | NOT NULL | 类型（如：MS:merchant_setting） |
| `ad_type_name` | varchar(35) |  | 类型名称（如：Merchant Setting） |
| `param_name` | varchar(55) |  | 参数名称（如：DirectPay） |
| `param_key` | varchar(125) | NOT NULL | 参数键（如：support_direct_pay） |
| `param_value` | varchar(550) | NOT NULL | 参数值（如：Y） |
| `memo` | varchar(255) |  | 备注 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
