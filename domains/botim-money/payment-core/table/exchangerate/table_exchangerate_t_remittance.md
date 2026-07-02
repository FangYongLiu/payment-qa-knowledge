---
id: tbl_exchangerate_t_remittance
object_type: Table
name: t_remittance (t_remittance)
aliases: [t_remittance, exchangerate.t_remittance]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: exchangerate schema DDL
tags: [payment-core, exchangerate]
sensitivity: normal
related_services: []
---

# t_remittance (t_remittance)

## 用途
物理表 `exchangerate.t_remittance`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | 待补 · 可空 |
| `currency_code_from` | varchar(20) | 待补 |
| `currency_code_to` | varchar(20) | 待补 |
| `value` | varchar(30) | 待补 |
| `cost` | double | 待补 · 可空 |
| `inverse_value` | decimal | 待补 · 可空 |
| `gmt_create` | bigint | 待补 |
| `image_name` | varchar(50) | 待补 · 可空 |
| `platform` | varchar(30) | 待补 · 可空 |
| `batch` | int | 待补 · 可空 |
| `extend1` | varchar(300) | 待补 · 可空 |
| `extend2` | varchar(1500) | 待补 · 可空 |
| `country` | varchar(40) | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_gmt_create`:gmt_create
- `idx_platform_currency_code_to_gmt_create`:platform, currency_code_to, gmt_create

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
