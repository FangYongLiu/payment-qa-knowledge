---
id: tbl_reconciliation_t_fee_total_summary
object_type: Table
name: 手续费总额汇总表 (t_fee_total_summary)
aliases: [t_fee_total_summary, reconciliation.t_fee_total_summary]
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

# 手续费总额汇总表 (t_fee_total_summary)

## 用途
物理表 `reconciliation.t_fee_total_summary`,主键 `id`。手续费总额汇总表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `fund_channel_code` | varchar(32) | 渠道编号 |
| `biz_type` | varchar(3) | 业务类型 |
| `bill_date` | varchar(8) | 对账日期 |
| `clear_flow_count` | int | 清算流水总笔数 · 可空 |
| `fund_flow_count` | int | 入账流水总笔数 · 可空 |
| `clear_fee_amount` | decimal(15, 4) | 清算流水手续费总额 · 可空 |
| `fund_fee_amount` | decimal(15, 4) | 入账流水手续费总额 · 可空 |
| `diff_fee_amount` | decimal(15, 4) | 差异手续费 · 可空 |
| `fx_gain_loss` | decimal(19, 4) | FX Gain/Loss  · 可空 |
| `fee_entry_status` | char | 手续费结转状态 S-成功, P-处理中, F-失败 · 可空 |
| `fee_carry_amount` | decimal(15, 4) | 手续费结转金额 · 可空 |
| `fee_carry_message` | varchar(255) | 手续费结转信息 · 可空 |
| `fee_voucher_no` | varchar(64) | 手续费结转凭证号 · 可空 |
| `clear_vat_amount` | decimal(15, 4) | 清算流水增值税总额 · 可空 |
| `fund_vat_amount` | decimal(15, 4) | 入账流水增值税总额 · 可空 |
| `diff_vat_amount` | decimal(15, 4) | 差异增值税 · 可空 |
| `vat_entry_status` | char | 增值税结转状态 S-成功, P-处理中, F-失败 · 可空 |
| `vat_carry_amount` | decimal(15, 4) | 增值税结转金额 · 可空 |
| `vat_carry_message` | varchar(255) | 增值税结转信息 · 可空 |
| `vat_voucher_no` | varchar(64) | 增值税结转凭证号 · 可空 |
| `status` | char | 汇总状态 S-成功, F-失败, E-已修改, C-已结转 · 可空 |
| `currency` | char(3) | 币种 · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
