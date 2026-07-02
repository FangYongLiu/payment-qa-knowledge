---
id: tbl_loyalty_t_audience_members_02
object_type: Table
name: t_audience_members_02 (t_audience_members_02)
aliases: [t_audience_members_02, loyalty.t_audience_members_02]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: loyalty schema DDL
tags: [marketing, loyalty]
sensitivity: normal
related_services: []
---

# t_audience_members_02 (t_audience_members_02)

## 用途
物理表 `loyalty.t_audience_members_02`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | 待补 · 可空 |
| `audience_id` | bigint unsigned | 待补 |
| `integration_id` | varchar(105) | 待补 |
| `created_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_audience_member`:audience_id, integration_id (UNIQUE)
- `idx_integration_id`:integration_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
