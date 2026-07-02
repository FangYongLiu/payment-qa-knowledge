---
id: tbl_merchant_t_merchant_dcc_config_audit
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
- t_merchant_dcc_config_audit
subdomain: merchant
module: null
sensitivity: normal
name: Merchant DCC Configuration Audit(t_merchant_dcc_config_audit)
aliases:
- t_merchant_dcc_config_audit
related_services:
- svc_merchant
related_scenarios: []
---
# Merchant DCC Configuration Audit(t_merchant_dcc_config_audit)

## 用途
Merchant DCC Configuration Audit。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary key |
| `config_id` | bigint |  | Reference to original config ID (null for deleted records) |
| `merchant_mid` | varchar(50) | NOT NULL | Merchant MID |
| `merchant_name` | varchar(128) |  | Merchant name |
| `config_type` | varchar(30) | NOT NULL | Configuration type |
| `operation_type` | varchar(20) | NOT NULL | Operation type (CREATE, UPDATE, DELETE) |
| `old_value` | varchar(128) |  | Value before change (null for CREATE) |
| `new_value` | varchar(128) |  | Value after change (null for DELETE) |
| `before_snapshot` | varchar(255) |  | Complete snapshot before change (JSON) |
| `after_snapshot` | varchar(255) |  | Complete snapshot after change (JSON) |
| `operator` | varchar(100) | NOT NULL | Operator who performed the action |
| `source` | varchar(50) |  | Source system/application |
| `audit_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Audit timestamp |
| `remarks` | varchar(255) |  | Additional remarks |
| `created_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Creation timestamp |
| `last_updated_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Last Updated Time |
| `data_version` | bigint | 默认 1 | Data version for concurrency control |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
