---
id: tbl_creditinvoice_t_tax_invoice
object_type: Table
name: 发票明细表 (t_tax_invoice)
aliases: [t_tax_invoice, creditinvoice.t_tax_invoice]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: creditinvoice schema DDL
tags: [lending, creditinvoice]
sensitivity: normal
related_services: []
---

# 发票明细表 (t_tax_invoice)

## 用途
物理表 `creditinvoice.t_tax_invoice`,主键 `id`。发票明细表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 自增id · 可空 |
| `invoice_no` | varchar(64) | 发票号 |
| `product_code` | varchar(64) | 产品码 |
| `invoice_type` | tinyint | 待补 |
| `file_tag` | varchar(128) | 发票pdf在ufs中的文件tag或路径 |
| `template_id` | bigint | 模板表的id |
| `income_id` | int | 收入对应的id（t_income表的id） · 可空 |
| `data` | varchar(1024) | 发票中的数据 |
| `ref_busi_no` | varchar(64) | 待补 |
| `busi_entity_no` | varchar(64) | 发票关联的业务主体no |
| `status` | smallint(2) | 发票状态 枚举值:(1有效 , -1失效) |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_in`:invoice_no (UNIQUE)
- `uk_rbn`:ref_busi_no, invoice_type, product_code (UNIQUE)
- `idx_eo`:busi_entity_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
