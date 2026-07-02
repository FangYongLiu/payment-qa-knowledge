---
id: tbl_cashdesk_t_audit
object_type: Table
name: 审核表 (t_audit)
aliases: [t_audit, cashdesk.t_audit]
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

# 审核表 (t_audit)

## 用途
物理表 `cashdesk.t_audit`,主键 `id`。审核表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `audit_type` | char | 审核类型（1：商户组配置 2.新增策略方案 3：维护策略方案） |
| `audit_title` | varchar(150) | 审核标题 · 可空 |
| `status` | char | 状态（W:待审核 S:审核通过 R:审核拒绝） |
| `apply_user` | varchar(50) | 申请人 · 可空 |
| `gmt_created` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
