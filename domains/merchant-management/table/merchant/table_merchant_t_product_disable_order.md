---
id: tbl_merchant_t_product_disable_order
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
- t_product_disable_order
subdomain: merchant
module: null
sensitivity: normal
name: Product disable order queue for job processing(t_product_disable_order)
aliases:
- t_product_disable_order
related_services:
- svc_merchant
related_scenarios: []
---
# Product disable order queue for job processing(t_product_disable_order)

## 用途
Product disable order queue for job processing。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary Key |
| `order_id` | varchar(64) | NOT NULL | Unique disable order ID |
| `merchant_mid` | varchar(32) | NOT NULL | Merchant ID |
| `package_code` | varchar(64) | NOT NULL | Package code to disable |
| `package_name` | varchar(128) |  | Package name |
| `action_type` | varchar(32) | NOT NULL / 默认 'DISABLE' | Action type (DISABLE/ENABLE) |
| `gmt_invalid` | timestamp |  | Expiration Time |
| `status` | varchar(32) | NOT NULL / 默认 'INIT' | Processing status (INIT/PROCESSING/SUCCESS/FAILED) |
| `error_message` | varchar(255) |  | Error details if failed |
| `retry_count` | int | 默认 0 | Number of retry attempts |
| `max_retries` | int | 默认 3 | Maximum retry limit |
| `processed_time` | timestamp |  | Actual processing time |
| `created_time` | timestamp |  | Created time |
| `last_updated_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Last updated time |
| `data_version` | bigint | NOT NULL / 默认 0 | Data version |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_created_time` (created_time)
  - `idx_merchant_mid` (merchant_mid)
  - `idx_processed_status` (processed_time, status)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
