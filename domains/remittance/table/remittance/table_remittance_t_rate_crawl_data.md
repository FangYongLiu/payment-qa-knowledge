---
id: tbl_remittance_t_rate_crawl_data
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_rate_crawl_data
subdomain: remittance
module: null
sensitivity: normal
name: t_rate_crawl_data
aliases:
- t_rate_crawl_data
related_services:
- svc_remittance
related_scenarios: []
---
# t_rate_crawl_data

## 用途
待补。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Unique identifier for each rate record |
| `source` | varchar(12) | NOT NULL | Source of the exchange rate data (e.g., western, wise, remitly) |
| `base_currency` | char(3) | NOT NULL | Source currency code in ISO 4217 format (e.g., USD, EUR) |
| `target_currency` | char(3) | NOT NULL | Target currency code in ISO 4217 format (e.g., CNY, INR) |
| `send_amount` | decimal(20,2) | NOT NULL | Amount in base currency to be exchanged |
| `rate` | decimal(20,10) | NOT NULL | Exchange rate from base currency to target currency |
| `update_at` | timestamp | NOT NULL | Timestamp when the rate was last updated by the source |
| `transfer_type` | varchar(20) |  | Type of transfer service (e.g., BANK_TRANSFER, MONEY_IN_MINUTES) |
| `created_at` | timestamp | NOT NULL | Timestamp when this record was created in the database |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_currencies` (base_currency, target_currency)
  - `idx_source` (source)
  - `idx_update_at` (update_at)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
