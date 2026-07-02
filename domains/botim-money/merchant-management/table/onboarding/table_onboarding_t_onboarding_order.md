---
id: tbl_onboarding_t_onboarding_order
object_type: Table
name: onboarding_order (t_onboarding_order)
aliases: [t_onboarding_order, onboarding.t_onboarding_order]
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

# onboarding_order (t_onboarding_order)

## 用途
物理表 `onboarding.t_onboarding_order`,主键 `id`。onboarding_order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 8+9 |
| `owner_id` | varchar(50) | ownerId |
| `type` | varchar(50) | ruleType |
| `fund_provider_code` | varchar(50) | fund_provider_code |
| `parent_order_type` | varchar(50) | parent_order_type · 可空 |
| `parent_order_id` | bigint | parent_order_id · 可空 |
| `item_id` | bigint | itemId · 可空 |
| `spawn` | varchar(16) | spawn |
| `status` | varchar(50) | status |
| `fail_code` | varchar(50) | failCode · 可空 |
| `fail_message` | varchar(200) | failMessage · 可空 |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |
| `sub_order_count` | int | sub_order_count · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_obd_owner`:owner_id
- `i_obd_parent`:parent_order_type, parent_order_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
