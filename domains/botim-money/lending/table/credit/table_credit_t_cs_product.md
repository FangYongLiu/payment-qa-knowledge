---
id: tbl_credit_t_cs_product
object_type: Table
name: 信贷产品定义表 (t_cs_product)
aliases: [t_cs_product, credit.t_cs_product]
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

# 信贷产品定义表 (t_cs_product)

## 用途
物理表 `credit.t_cs_product`,主键 `id`。信贷产品定义表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | 待补 · 可空 |
| `product_name` | varchar(128) | 产品名称 |
| `product_desc` | varchar(255) | 产品描述 · 可空 |
| `version` | smallint | 待补 |
| `product_type` | varchar(32) | 待补 |
| `inst_num` | smallint | 产品的期数 |
| `time_amount_per_inst` | smallint | 每期有多少个时间单位 |
| `time_unit` | smallint | 待补 |
| `processing_fee_rate` | decimal(10, 4) | 扣头息费率 |
| `monthly_interest_rate` | decimal(15, 4) | monthly rate · 可空 |
| `processing_fee_fix` | decimal(15, 2) | fix process fee |
| `processing_fee_cap` | decimal(10, 2) | 最高扣头息金额 · 可空 |
| `total_interest_rate` | decimal(10, 4) | 总利息 |
| `status` | smallint | 待补 |
| `use_condition` | varchar(1024) | 待补 |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_nv`:product_name, version (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
