---
id: tbl_cashdesk_t_audit_result
object_type: Table
name: 审核结果表 (t_audit_result)
aliases: [t_audit_result, cashdesk.t_audit_result]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cashdesk schema DDL
tags: [payment-tool, cashdesk]
sensitivity: normal
related_services: []
---

# 审核结果表 (t_audit_result)

## 用途
物理表 `cashdesk.t_audit_result`,主键 `id`。审核结果表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `audit_id` | bigint(18) | 审核id |
| `audit_result` | char | 审核结果（S:同意 R:拒绝） |
| `memo` | varchar(150) | 备注 · 可空 |
| `audit_user` | varchar(50) | 审核人 |
| `gmt_created` | timestamp | 创建时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_audit_id`:audit_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
