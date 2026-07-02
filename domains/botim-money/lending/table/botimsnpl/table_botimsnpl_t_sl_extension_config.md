---
id: tbl_botimsnpl_t_sl_extension_config
object_type: Table
name: t_sl_extension_config (t_sl_extension_config)
aliases: [t_sl_extension_config, botimsnpl.t_sl_extension_config]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# t_sl_extension_config (t_sl_extension_config)

## 用途
物理表 `botimsnpl.t_sl_extension_config`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `extension_days` | int(10) | Extension period in days (e.g. 7) |
| `fee_rate` | decimal(10, 4) | Fee rate (e.g. 0.0800 = 8%) |
| `min_fee` | decimal(15, 2) | Minimum fee cap (e.g. 20.00 AED) |
| `max_fee` | decimal(15, 2) | Maximum fee cap (e.g. 500.00 AED) |
| `vat_rate` | decimal(10, 4) | VAT rate (e.g. 0.0500 = 5%) |
| `status` | tinyint | 1=Active, 0=Disabled |
| `version` | int(10) | extension config version |
| `ext` | varchar(255) | ext · 可空 |
| `created_time` | timestamp | created time |
| `last_modified` | timestamp | last modified time |

## 主键 / 索引
- 主键:`id`
- `idx_extension_days`:extension_days

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
