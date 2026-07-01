---
id: tbl_ppcenter_t_merchant_config_relation
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
- t_merchant_config_relation
subdomain: pricing
module: null
sensitivity: normal
name: 商户配置关系(t_merchant_config_relation)
aliases:
- t_merchant_config_relation
related_services:
- svc_ppcenter
related_scenarios: []
---
# 商户配置关系(t_merchant_config_relation)

## 用途
商户配置关系。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int(12) | PK / AUTO_INC | 主键 |
| `config_type` | varchar(32) | NOT NULL | 配置类型 1:算费；2:结算周期 |
| `product_order_id` | int(12) | NOT NULL | 开通记录表关联id |
| `relation_id` | int(12) | NOT NULL | 关联配置值 |
| `status` | tinyint(2) | NOT NULL | 1:生效；0:失效 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `inx_product_order_id` (product_order_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
