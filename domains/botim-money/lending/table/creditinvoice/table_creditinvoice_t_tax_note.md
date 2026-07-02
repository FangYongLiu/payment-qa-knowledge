---
id: tbl_creditinvoice_t_tax_note
object_type: Table
name: 减免记录id/退票id 与 ref_invoice_id 组成唯一索引 (t_tax_note)
aliases: [t_tax_note, creditinvoice.t_tax_note]
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

# 减免记录id/退票id 与 ref_invoice_id 组成唯一索引 (t_tax_note)

## 用途
物理表 `creditinvoice.t_tax_note`,主键 `id`。减免记录id/退票id 与 ref_invoice_id 组成唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 自增id · 可空 |
| `tcn_no` | varchar(64) | 发票号 |
| `tcn_type` | int(10) | tcn类型 2:放款退票tcn,4:减免抵扣收入tcn,6:discount 抵扣收入tcn,8:还款退回，tcn.10:installmentfee 税退回 |
| `file_tag` | varchar(128) | 发票pdf在ufs中的文件tag或路径 |
| `template_id` | int(128) | 模板表自增id |
| `deduct_income_id` | int | 抵扣记录id（t_deductible_income 表的id) · 可空 |
| `data` | varchar(1024) | note中的数据 |
| `ref_busi_no` | varchar(128) | tcn_type=2时:被退票的借款订单的order_no,tcn_type=4时:减免记录id,tcn_type=6时:优惠券记录id,tcn_type=8时:引起退票的退票订单id 为保持历史数据兼容性，保留此字段, tcn_type=10 时:发票 id |
| `ref_invoice_id` | varchar(64) | 关联的发票id |
| `status` | smallint(4) | 待补 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_dii`:deduct_income_id (UNIQUE)
- `idx_rii`:ref_invoice_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
