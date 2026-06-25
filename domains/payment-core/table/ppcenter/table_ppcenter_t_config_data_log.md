---
id: tbl_ppcenter_t_config_data_log
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
- t_config_data_log
subdomain: pricing
module: null
sensitivity: normal
name: 配置数据日志(t_config_data_log)
aliases:
- t_config_data_log
related_services:
- svc_ppcenter
related_scenarios: []
---
# 配置数据日志(t_config_data_log)

## 用途
配置数据日志。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int(12) | PK / AUTO_INC | primary key |
| `config_type` | varchar(12) |  | config type |
| `gmt_effective` | timestamp |  | effective time |
| `gmt_invalid` | timestamp |  | invalid time |
| `gmt_create` | timestamp | NOT NULL | create time |
| `gmt_modify` | timestamp | NOT NULL | update time |
| `product_order_id` | int(12) | NOT NULL | relation t_merchant_product_order id |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
