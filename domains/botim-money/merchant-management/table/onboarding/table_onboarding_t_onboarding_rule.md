---
id: tbl_onboarding_t_onboarding_rule
object_type: Table
name: onboarding_rule (t_onboarding_rule)
aliases: [t_onboarding_rule, onboarding.t_onboarding_rule]
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

# onboarding_rule (t_onboarding_rule)

## 用途
物理表 `onboarding.t_onboarding_rule`,主键 `id`。onboarding_rule。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `type` | varchar(50) | ruleType |
| `fund_provider_code` | varchar(50) | fund_provider_code |
| `created_time` | timestamp(3) | created_time |

## 主键 / 索引
- 主键:`id`
- `uk_or_type`:fund_provider_code, type (UNIQUE)
- `i_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
