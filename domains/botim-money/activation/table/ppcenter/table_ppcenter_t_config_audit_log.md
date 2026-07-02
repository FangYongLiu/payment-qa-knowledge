---
id: tbl_ppcenter_t_config_audit_log
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
- t_config_audit_log
subdomain: pricing
module: null
sensitivity: normal
name: 配置审核日志(t_config_audit_log)
aliases:
- t_config_audit_log
related_services:
- svc_ppcenter
related_scenarios: []
---
# 配置审核日志(t_config_audit_log)

## 用途
配置审核日志。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int(16) | PK / AUTO_INC | 主键 |
| `apply_id` | int | NOT NULL | 申请id |
| `status` | varchar(2) | NOT NULL | 审批状态 S:审核通过 R:审核拒绝 |
| `auditor` | varchar(64) | NOT NULL | 审批人 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp |  | 修改时间 |
| `memo` | varchar(255) |  | 备注 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
