---
id: tbl_onboarding_t_item
object_type: Table
name: item (t_item)
aliases: [t_item, onboarding.t_item]
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

# item (t_item)

## 用途
物理表 `onboarding.t_item`,主键 `id`。item。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `owner_id` | varchar(50) | owner_id |
| `type` | varchar(50) | item_type |
| `lock_order_id` | bigint | lock_order_id · 可空 |
| `fund_provider_code` | varchar(50) | fund_provider_code |
| `status` | varchar(50) | status |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |
| `fail_message` | varchar(128) | fail_message · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_item_owner_pf`:owner_id, fund_provider_code, type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
