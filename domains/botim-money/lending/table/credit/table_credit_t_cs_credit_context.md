---
id: tbl_credit_t_cs_credit_context
object_type: Table
name: 授信上下文 (t_cs_credit_context)
aliases: [t_cs_credit_context, credit.t_cs_credit_context]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# 授信上下文 (t_cs_credit_context)

## 用途
物理表 `credit.t_cs_credit_context`,主键 `id`。授信上下文。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `channel` | varchar(20) | 渠道 |
| `device_snap` | varchar(10000) | 待补 · 可空 |
| `ip` | varchar(30) | 待补 · 可空 |
| `profile_snap` | varchar(10000) | 待补 · 可空 |
| `credit_id` | int | 授信ID |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 更新时间 · 可空 |
| `user_behavior_id` | bigint | t_user_behavior_log.id · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_credit_id`:credit_id
- `idx_ip`:ip

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
