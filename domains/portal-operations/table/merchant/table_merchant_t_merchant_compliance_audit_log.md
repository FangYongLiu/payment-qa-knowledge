---
id: tbl_merchant_t_merchant_compliance_audit_log
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
- t_merchant_compliance_audit_log
subdomain: merchant
module: null
sensitivity: normal
name: 商户合规审计日志(t_merchant_compliance_audit_log)
aliases:
- t_merchant_compliance_audit_log
related_services:
- svc_merchant
related_scenarios: []
---
# 商户合规审计日志(t_merchant_compliance_audit_log)

## 用途
商户合规审计日志。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | identifier |
| `merchant_mid` | varchar(50) | NOT NULL | Merchant ID |
| `merchant_name` | varchar(255) | NOT NULL | Merchant Name |
| `compliance_type` | varchar(50) | NOT NULL | Compliance Type |
| `action` | varchar(50) | NOT NULL | Action |
| `action_time` | timestamp | NOT NULL | Action Time |
| `notification_recipient` | varchar(250) |  | Notification Recipient |
| `operator` | varchar(100) | NOT NULL | Operator |
| `created_time` | timestamp | NOT NULL | Created Time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_merchant_mid` (merchant_mid)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
