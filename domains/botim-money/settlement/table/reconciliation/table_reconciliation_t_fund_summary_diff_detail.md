---
id: tbl_reconciliation_t_fund_summary_diff_detail
object_type: Table
name: 资金对账差异明细表 (t_fund_summary_diff_detail)
aliases: [t_fund_summary_diff_detail, reconciliation.t_fund_summary_diff_detail]
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

# 资金对账差异明细表 (t_fund_summary_diff_detail)

## 用途
物理表 `reconciliation.t_fund_summary_diff_detail`,主键 `id`。资金对账差异明细表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `bank_code` | varchar(15) | Bank Code · 可空 |
| `bill_date` | varchar(8) | 对账日期 |
| `fund_trans_type` | varchar(30) | Fund Trans Type · 可空 |
| `fail_type` | varchar(16) | 失败类型 BREU:银收企未收 EPBU:企付银未付 BPEU:银付企未付 ERBU:企收银未收 |
| `amount` | decimal(15, 4) | 金额 |
| `currency` | char(3) | 币种 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `index_billDate_transtype`:bank_code, bill_date, fund_trans_type

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
