---
id: tbl_creditinvoice_t_accounting_entry
object_type: Table
name: 会计科目表 (t_accounting_entry)
aliases: [t_accounting_entry, creditinvoice.t_accounting_entry]
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

# 会计科目表 (t_accounting_entry)

## 用途
物理表 `creditinvoice.t_accounting_entry`,主键 `id`。会计科目表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `entry_number` | varchar(32) | 科目号 |
| `entry_type` | varchar(32) | 待补 |
| `summary_entry_name` | varchar(32) | 概要科目名称 |
| `entry_name` | varchar(64) | 科目英文名称 |
| `entry_ch_name` | varchar(64) | 科目中文名 |
| `direction` | char(6) | 余额方向，记账时对应科目在debit中出现时金额表示增加则取值为debit，否则为credit |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
