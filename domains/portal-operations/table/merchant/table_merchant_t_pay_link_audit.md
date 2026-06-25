---
id: tbl_merchant_t_pay_link_audit
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
- t_pay_link_audit
subdomain: merchant
module: null
sensitivity: normal
name: pay link audit table(t_pay_link_audit)
aliases:
- t_pay_link_audit
related_services:
- svc_merchant
related_scenarios: []
---
# pay link audit table(t_pay_link_audit)

## 用途
pay link audit table。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `pay_link_status_id` | bigint | NOT NULL | payLink status id |
| `merchant_id` | bigint | NOT NULL | merchant id |
| `merchant_mid` | varchar(32) | NOT NULL | merchant mid |
| `applicant` | varchar(100) | NOT NULL | applicant |
| `applicant_id` | varchar(32) | NOT NULL | applicant id |
| `apply_reason` | varchar(255) | NOT NULL | apply reason |
| `auditor` | varchar(100) |  | auditor |
| `auditor_id` | varchar(32) |  | auditor id |
| `audit_reason` | varchar(255) |  | audit reason |
| `from_pos_status` | varchar(10) |  | from pos status |
| `to_pos_status` | varchar(10) | NOT NULL | to pos status |
| `fromecom_status` | varchar(10) |  | from e-com status |
| `toecom_status` | varchar(10) | NOT NULL | to e-com status |
| `status` | varchar(10) | NOT NULL | status |
| `audit_time` | timestamp |  | create time |
| `created_time` | timestamp | NOT NULL | create time |
| `last_updated_time` | timestamp | NOT NULL | last update time |
| `data_version` | bigint | NOT NULL | data version |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `merchant_mid_idx` (merchant_mid)
  - `pay_link_status_id_idx` (pay_link_status_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
