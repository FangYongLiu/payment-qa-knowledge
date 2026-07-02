---
id: tbl_basiscustomer_t_rate_range_setting
object_type: Table
name: Rate Range Settings - Currency-level guardrails for Rate Master (t_rate_range_setting)
aliases: [t_rate_range_setting, basiscustomer.t_rate_range_setting]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basiscustomer schema DDL
tags: [activation, basiscustomer]
sensitivity: normal
related_services: []
---

# Rate Range Settings - Currency-level guardrails for Rate Master (t_rate_range_setting)

## 用途
物理表 `basiscustomer.t_rate_range_setting`,主键 `id`。Rate Range Settings - Currency-level guardrails for Rate Master。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | 待补 · 可空 |
| `currency` | char(3) | Currency code (e.g., CNY, INR) |
| `direction` | tinyint | Rate direction: 0=AED_TO_FCY, 1=FCY_TO_AED |
| `min_rate` | decimal(18, 6) | Minimum allowed rate |
| `max_rate` | decimal(18, 6) | Maximum allowed rate |
| `status` | varchar(12) | Status: ACTIVE, INACTIVE |
| `created_by` | varchar(50) | User who created the record |
| `create_time` | timestamp | Creation timestamp |
| `updated_by` | varchar(50) | User who last updated the record · 可空 |
| `update_time` | timestamp | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uniq_currency_direction`:currency, direction (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
