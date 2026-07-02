---
id: tbl_collection_t_ia_refuse_reason
object_type: Table
name: 拒绝原因 (t_ia_refuse_reason)
aliases: [t_ia_refuse_reason, collection.t_ia_refuse_reason]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 拒绝原因 (t_ia_refuse_reason)

## 用途
物理表 `collection.t_ia_refuse_reason`,主键 `id`。拒绝原因。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(64) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(64) | 更新人员 · 可空 |
| `app_id` | varchar(64) | 进件id · 可空 |
| `audit_uid` | varchar(64) | 审核id · 可空 |
| `collection_uid` | varchar(64) | 分配id · 可空 |
| `type` | tinyint(3) | 类型1 资料 2收入 · 可空 |
| `reason` | varchar(150) | 拒绝原因 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_application_id`:app_id
- `idx_audit_uid`:audit_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
