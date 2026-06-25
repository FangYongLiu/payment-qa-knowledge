---
id: tbl_merchant_t_fee_type
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
- t_fee_type
subdomain: merchant
module: null
sensitivity: normal
name: Fee Type Catalog(t_fee_type)
aliases:
- t_fee_type
related_services:
- svc_merchant
related_scenarios: []
---
# Fee Type Catalog(t_fee_type)

## 用途
Fee Type Catalog。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Row Id |
| `fee_name` | varchar(30) | NOT NULL | Fee name |
| `fee_description` | varchar(200) |  | Fee description |
| `gl_account_no` | varchar(50) |  | GL Account Number |
| `vat_applicability` | tinyint(1) | NOT NULL | VAT Applicability (0=No, 1=Yes) |
| `default_amount` | decimal(9,2) |  | Default Amount |
| `status` | varchar(10) | NOT NULL | Status |
| `data_version` | bigint | NOT NULL | Data Version |
| `created_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Record creation time |
| `last_updated_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Last Updated Time |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_fee_name` 唯一 (fee_name)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
