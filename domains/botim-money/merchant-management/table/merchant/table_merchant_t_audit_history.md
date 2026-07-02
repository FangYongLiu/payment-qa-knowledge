---
id: tbl_merchant_t_audit_history
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
- t_audit_history
subdomain: merchant
module: null
sensitivity: normal
name: 审批历史(t_audit_history)
aliases:
- t_audit_history
related_services:
- svc_merchant
related_scenarios: []
---
# 审批历史(t_audit_history)

## 用途
审批历史。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `merchant_creation_id` | bigint | NOT NULL | 商户创建id |
| `auditor_mid` | varchar(50) | NOT NULL | 审批者会员id |
| `auditor_name` | varchar(50) |  | Auditor Name |
| `result` | varchar(20) | NOT NULL | 审批结果 PASS  REJECT |
| `comments` | varchar(200) | NOT NULL | 审批意见 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `flow_status` | varchar(16) |  | Flow Status |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
