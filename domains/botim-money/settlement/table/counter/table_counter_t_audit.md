---
id: tbl_counter_t_audit
object_type: Table
name: 审核表 (t_audit)
aliases: [t_audit, counter.t_audit]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 审核表 (t_audit)

## 用途
物理表 `counter.t_audit`,主键 `audit_id`。审核表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `audit_id` | bigint(17) | 主键 8+9 17位 |
| `audit_type` | varchar(16) | 审核类型 · 可空 |
| `parent_id` | bigint | 父ID 批量审核需该字段 · 可空 |
| `voucher_id` | bigint | 凭证id · 可空 |
| `biz_id` | bigint(17) | 业务编号 · 可空 |
| `auditor` | varchar(32) | 审核者 · 可空 |
| `status` | varchar(16) | 审核状态 A-审核中 D-审核拒绝 P-审核通过 · 可空 |
| `execute_status` | char | 执行状态: P-执行中 S-成功 F-失败 · 可空 |
| `applier` | varchar(32) | 申请人 · 可空 |
| `assignee` | varchar(255) | Assignee · 可空 |
| `memo` | varchar(512) | 备注 · 可空 |
| `audit_memo` | varchar(512) | 审核人备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`audit_id`
- `index_parent_id`:parent_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
