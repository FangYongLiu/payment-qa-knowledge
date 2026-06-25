---
id: tbl_merchant_t_product_item_info
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
- t_product_item_info
subdomain: merchant
module: null
sensitivity: normal
name: 商户产品项信息(t_product_item_info)
aliases:
- t_product_item_info
related_services:
- svc_merchant
related_scenarios: []
---
# 商户产品项信息(t_product_item_info)

## 用途
商户产品项信息。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC |  |
| `merchant_creation_id` | bigint | NOT NULL | Merchant Creation Id |
| `product` | varchar(50) |  | Product Name |
| `sales_percentage` | varchar(10) |  | Sales Percentage |
| `created_time` | timestamp | 默认 CURRENT_TIMESTAMP | Created At Time |
| `last_updated_time` | timestamp | 默认 CURRENT_TIMESTAMP | Last Updated Time |
| `data_version` | bigint | 默认 1 | Data version for concurrency control |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_merchant_creation_id` (merchant_creation_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
