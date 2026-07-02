---
id: tbl_basicrcdata_t_leantech_installment_fee_config
object_type: Table
name: Installment and processing fee config (t_leantech_installment_fee_config)
aliases: [t_leantech_installment_fee_config, basicrcdata.t_leantech_installment_fee_config]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basicrcdata schema DDL
tags: [risk, basicrcdata]
sensitivity: normal
related_services: []
---

# Installment and processing fee config (t_leantech_installment_fee_config)

## 用途
物理表 `basicrcdata.t_leantech_installment_fee_config`,主键 `id`。Installment and processing fee config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `rating` | varchar(10) | Risk rating (A–E) |
| `term` | int | Installment term (months) |
| `rxt_code` | varchar(20) | Rate code (RxT) |
| `installment_fee_rate` | decimal(10, 4) | Installment fee rate · 可空 |
| `processing_fee_rate` | decimal(10, 4) | Processing fee rate · 可空 |
| `create_time` | timestamp | Creation time |
| `update_time` | timestamp | Last updated |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
