---
id: tbl_reconciliation_t_fee_summary
object_type: Table
name: 手续费对账汇总 手续费对账汇总 (t_fee_summary)
aliases: [t_fee_summary, reconciliation.t_fee_summary]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 手续费对账汇总 手续费对账汇总 (t_fee_summary)

## 用途
物理表 `reconciliation.t_fee_summary`,主键 `summary_id`。手续费对账汇总 手续费对账汇总。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `summary_id` | bigint(17) | 汇总ID |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(3) | 业务类型 · 可空 |
| `start_time` | varchar(8) | 起始日期 手续费对账起始时间yyyyMMdd · 可空 |
| `end_time` | varchar(8) | 截止日期 手续费对账截止时间yyyyMMdd · 可空 |
| `count` | int(10) | 总笔数 · 可空 |
| `amount` | decimal(15, 2) | 总金额 · 可空 |
| `fee_amount` | decimal(15, 4) | 手续费 · 可空 |
| `vat_amount` | decimal(15, 4) | 增值税 · 可空 |
| `diff_count` | int(10) | 差异笔数 · 可空 |
| `diff_fee_amount` | decimal(15, 4) | 差异手续费 · 可空 |
| `diff_vat_amount` | decimal(15, 4) | 差异增值税 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `status` | varchar(4) | 手续费对账汇总状态 · 可空 |
| `fee_entry_status` | varchar(4) | 手续费结转状态 · 可空 |
| `vat_entry_status` | varchar(4) | 增值税结转状态 · 可空 |
| `fee_entry_message` | varchar(255) | 手续费结转信息 · 可空 |
| `vat_entry_message` | varchar(255) | 增值税结转信息 · 可空 |
| `carry_fee_amount` | decimal(15, 2) | 手续费实际结转金额 · 可空 |
| `carry_vat_amount` | decimal(15, 2) | 增值税实际结转金额 · 可空 |
| `fee_voucher_no` | varchar(64) | 手续费凭证编号 · 可空 |
| `vat_voucher_no` | varchar(64) | 增值税凭证编号 · 可空 |

## 主键 / 索引
- 主键:`summary_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
