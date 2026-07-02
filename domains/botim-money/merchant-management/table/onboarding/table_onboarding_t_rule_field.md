---
id: tbl_onboarding_t_rule_field
object_type: Table
name: rule_field (t_rule_field)
aliases: [t_rule_field, onboarding.t_rule_field]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: onboarding schema DDL
tags: [merchant-management, onboarding]
sensitivity: normal
related_services: []
---

# rule_field (t_rule_field)

## 用途
物理表 `onboarding.t_rule_field`,主键 `id`。rule_field。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `rule_id` | bigint | rule_id |
| `code` | varchar(128) | code |
| `mandatory` | varchar(20) | mandatory |
| `created_time` | timestamp(3) | created_time |

## 主键 / 索引
- 主键:`id`
- `uk_name`:rule_id, code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
