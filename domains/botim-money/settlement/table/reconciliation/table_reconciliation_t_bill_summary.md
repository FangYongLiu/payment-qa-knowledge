---
id: tbl_reconciliation_t_bill_summary
object_type: Table
name: 对账汇总单 (t_bill_summary)
aliases: [t_bill_summary, reconciliation.t_bill_summary]
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

# 对账汇总单 (t_bill_summary)

## 用途
物理表 `reconciliation.t_bill_summary`,主键 `id`。对账汇总单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `bill_batch_no` | varchar(32) | 对账批次编号 · 可空 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(16) | 业务类型 · 可空 |
| `bill_date` | varchar(8) | 对账日期 · 可空 |
| `status` | varchar(8) | 对账状态 · 可空 |
| `total_record` | int | 交易总笔数 · 可空 |
| `total_amount` | decimal(15, 2) | 交易总金额 · 可空 |
| `carried_amount` | decimal(15, 4) | 已结转金额 · 可空 |
| `uncarried_amount` | decimal(15, 4) | 待结转金额 · 可空 |
| `markup_amount` | decimal(19, 4) | Markup Amount · 可空 |
| `markup_carried_amount` | decimal(19, 4) | Markup Carried Amount · 可空 |
| `currency` | varchar(3) | 货币 币种 · 可空 |
| `success_record` | int | 交易成功总笔数 · 可空 |
| `success_amount` | decimal(15, 2) | 交易成功总金额 · 可空 |
| `different_record` | int | 差异笔数 · 可空 |
| `different_amount` | decimal(15, 2) | 差异金额 · 可空 |
| `settle_amount` | decimal(15, 4) | 结算金额 · 可空 |
| `settle_currency` | varchar(3) | 结算币种 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |
| `channel_type` | varchar(4) | 渠道类型: SC 供应商渠道 , FC 资金渠道 · 可空 |
| `notice_status` | varchar(4) | 通知状态 · 可空 |
| `notice_message` | varchar(255) | 通知结果信息 · 可空 |
| `voucher_no` | varchar(64) | 凭证编号 · 可空 |
| `extension` | varchar(255) | extension · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_channel_biz_date`:fund_channel_code, bill_date, biz_type (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
