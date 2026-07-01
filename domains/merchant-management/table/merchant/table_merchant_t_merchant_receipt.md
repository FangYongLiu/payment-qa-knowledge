---
id: tbl_merchant_t_merchant_receipt
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
- t_merchant_receipt
subdomain: merchant
module: null
sensitivity: normal
name: MerchantReceipt(t_merchant_receipt)
aliases:
- t_merchant_receipt
related_services:
- svc_merchant
related_scenarios: []
---
# MerchantReceipt(t_merchant_receipt)

## 用途
MerchantReceipt。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | ID |
| `merchant_mid` | varchar(50) | NOT NULL | merchant_mid |
| `logo` | varchar(100) |  | logo |
| `logo_enabled` | varchar(32) | NOT NULL | Customized Logo Enabled |
| `created_time` | timestamp | NOT NULL | created_time |
| `last_updated_time` | timestamp | NOT NULL | last_updated_time |
| `data_version` | bigint | NOT NULL | data_version |
| `customized_pos_logo_enabled` | tinyint(1) | 默认 0 | enable POS Logo |
| `customized_pos_logo` | varchar(100) |  | POS customized logo |
| `merchant_info_pos_enabled` | tinyint(1) | 默认 0 | Show merchant Info on POS |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `i_mr_mid` 唯一 (merchant_mid)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
