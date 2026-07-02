---
id: tbl_reconciliation_t_on_account_summary
object_type: Table
name: 挂账汇总表 (t_on_account_summary)
aliases: [t_on_account_summary, reconciliation.t_on_account_summary]
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

# 挂账汇总表 (t_on_account_summary)

## 用途
物理表 `reconciliation.t_on_account_summary`,主键 `id`。挂账汇总表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `transaction_type` | varchar(16) | Transaction Type BIZ: business VAM:VAM PAYBY_VAM:PAYBY_VAM |
| `source_date` | date | 来源日期 |
| `source_identity` | varchar(64) | Source Identity · 可空 |
| `method` | char | 挂帐方式 A:自动 M:手动 |
| `bank_date` | timestamp | 银行交易时间 · 可空 |
| `amount` | decimal(19, 4) | 金额 |
| `currency` | char(3) | 币种 |
| `write_off_amount` | decimal(19, 4) | 已销账金额 |
| `file_name` | varchar(255) | 文件名称 · 可空 |
| `status` | char(2) | 状态 WW: 待销账 PW:部分销账 FW:已销账 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_type_identity`:transaction_type, source_identity (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
