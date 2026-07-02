---
id: tbl_reconciliation_t_fee_summary_detail
object_type: Table
name: 手续费对账差错数据 手续费对账差错数据 (t_fee_summary_detail)
aliases: [t_fee_summary_detail, reconciliation.t_fee_summary_detail]
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

# 手续费对账差错数据 手续费对账差错数据 (t_fee_summary_detail)

## 用途
物理表 `reconciliation.t_fee_summary_detail`,主键 `detail_id`。手续费对账差错数据 手续费对账差错数据。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `detail_id` | bigint(17) | 差错数据ID |
| `summary_id` | bigint(17) | 汇总ID · 可空 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(3) | 业务类型 · 可空 |
| `inst_order_no` | varchar(32) | 机构订单号 · 可空 |
| `trade_amount` | decimal(15, 2) | 交易金额 · 可空 |
| `clear_amount` | decimal(15, 2) | 清算金额 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `trade_fee_amount` | decimal(15, 4) | 交易手续费 · 可空 |
| `clear_fee_amount` | decimal(15, 4) | 清算手续费 · 可空 |
| `trade_vat_amount` | decimal(15, 4) | 交易增值税 · 可空 |
| `clear_vat_amount` | decimal(15, 4) | 清算增值税 · 可空 |
| `bill_status` | varchar(3) | 资金对账状态 · 可空 |
| `fee_status` | varchar(3) | 手续费对账状态 差错流水状态 · 可空 |
| `message` | varchar(256) | 差错原因 差错数据原因 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`detail_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
