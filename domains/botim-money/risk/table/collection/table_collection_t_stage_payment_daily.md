---
id: tbl_collection_t_stage_payment_daily
object_type: Table
name: t_stage_payment_daily (t_stage_payment_daily)
aliases: [t_stage_payment_daily, collection.t_stage_payment_daily]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# t_stage_payment_daily (t_stage_payment_daily)

## 用途
物理表 `collection.t_stage_payment_daily`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Surrogate primary key · 可空 |
| `stat_date` | date | Business calendar date (stageParamDate) |
| `dept_id` | int | -1 = company-wide row; otherwise department id |
| `product_code` | int | Product code (single selection on UI) |
| `stage` | varchar(12) | Collection stage label (Stage column; StageEnum.value) |
| `query_type` | tinyint | 1 = Amount mode; 2 = Account (count) mode |
| `restructure` | tinyint | 0 = normal; 1 = restructure (productTag=restructure) |
| `amt_am0` | decimal(20, 4) | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
