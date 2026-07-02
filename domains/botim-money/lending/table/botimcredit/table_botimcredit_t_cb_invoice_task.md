---
id: tbl_botimcredit_t_cb_invoice_task
object_type: Table
name: Table for recording invoice creation, used for failure compensation. (t_cb_invoice_task)
aliases: [t_cb_invoice_task, botimcredit.t_cb_invoice_task]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimcredit schema DDL
tags: [lending, botimcredit]
sensitivity: normal
related_services: []
---

# Table for recording invoice creation, used for failure compensation. (t_cb_invoice_task)

## 用途
物理表 `botimcredit.t_cb_invoice_task`,主键 `id`。Table for recording invoice creation, used for failure compensation.。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `busi_entity_no` | varchar(255) | The business entity number associated with the invoice. Here, the business entity refers to the entity to which multiple invoices belong, such as the loan order number in CashNow. |
| `ref_busi_no` | varchar(64) | The unique identifier of the business corresponding to the invoice. |
| `type` | smallint(4) | 待补 |
| `detail` | varchar(1024) | Parameters used when calling the invoice interface, in JSON format. · 可空 |
| `status` | smallint(4) | 待补 |
| `invoice_nos` | varchar(64) | Invoice number or TCN number. TCN numbers may be multiple, separated by commas. · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_tn`:ref_busi_no, type (UNIQUE)
- `ix_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
