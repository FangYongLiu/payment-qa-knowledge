---
id: tbl_ppcenter_t_biz_product_tag
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- ppcenter
- pricing
- t_biz_product_tag
subdomain: pricing
module: null
sensitivity: normal
name: 业务产品标签(t_biz_product_tag)
aliases:
- t_biz_product_tag
related_services:
- svc_ppcenter
related_scenarios: []
---
# 业务产品标签(t_biz_product_tag)

## 用途
业务产品标签。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `biz_product_code` | varchar(64) | NOT NULL | 产品码 |
| `tag` | varchar(64) |  | 产品标签 |
| `tag_type` | varchar(16) |  | risk、风控 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
