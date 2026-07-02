---
id: tbl_botimsnpl_t_sl_product
object_type: Table
name: snpl product configuration table (t_sl_product)
aliases: [t_sl_product, botimsnpl.t_sl_product]
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

# snpl product configuration table (t_sl_product)

## 用途
物理表 `botimsnpl.t_sl_product`,主键 `id`。snpl product configuration table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | primary key · 可空 |
| `product_name` | varchar(30) | product name |
| `product_desc` | varchar(50) | product description |
| `version` | int(4) | version, always use latest version |
| `tenor` | int(4) | tenor |
| `flat_rate` | decimal(12, 6) | flat rate |
| `monthly_rate` | decimal(12, 6) | monthly rate |
| `applicable_conditions` | varchar(255) | json string |
| `status` | int(4) | 0-invalid,1-valid |
| `ext` | varchar(255) | ext · 可空 |
| `created_time` | datetime | created time |
| `last_modified` | datetime | last modified time |

## 主键 / 索引
- 主键:`id`
- `t_sl_product_prod_name_tenor_ver_uk`:product_name, tenor, version (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
