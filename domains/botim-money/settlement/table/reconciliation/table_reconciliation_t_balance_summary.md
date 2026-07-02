---
id: tbl_reconciliation_t_balance_summary
object_type: Table
name: 余额对账表 (t_balance_summary)
aliases: [t_balance_summary, reconciliation.t_balance_summary]
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

# 余额对账表 (t_balance_summary)

## 用途
物理表 `reconciliation.t_balance_summary`,主键 `id`。余额对账表。业务语义细节**待补**(表结构来自 DDL)。

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
| `report_type` | varchar(16) | 报表类型 |
| `opening_amount` | decimal(15, 2) | 日初金额 · 可空 |
| `change_amount` | decimal(15, 2) | 变化金额 · 可空 |
| `ending_amount` | decimal(15, 2) | 日终金额 · 可空 |
| `difference_status` | char | 差异状态 初始化:I 成功:S 失败:F |
| `report_url` | varchar(512) | 报表地址 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `unique_key`:bank_code, bill_date, report_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
