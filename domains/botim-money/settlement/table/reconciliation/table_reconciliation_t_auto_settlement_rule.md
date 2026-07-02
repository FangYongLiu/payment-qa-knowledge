---
id: tbl_reconciliation_t_auto_settlement_rule
object_type: Table
name: Auto Settlement Rule (t_auto_settlement_rule)
aliases: [t_auto_settlement_rule, reconciliation.t_auto_settlement_rule]
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

# Auto Settlement Rule (t_auto_settlement_rule)

## 用途
物理表 `reconciliation.t_auto_settlement_rule`,主键 `rule_id`。Auto Settlement Rule。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `rule_id` | int | Rule Id · 可空 |
| `rule_type` | varchar(10) | Rule Type |
| `rule_name` | varchar(32) | Rule Name |
| `rule_explanation` | varchar(512) | Rule Explanation · 可空 |
| `settlement_template_id` | int | Settlement Template Id |
| `rule_content` | varchar(1024) | Rule Content · 可空 |
| `settlement_amount_limit` | decimal(19, 4) | Settlement Amount Limit · 可空 |
| `settlement_currency` | char(3) | Settlement Currency |
| `cron` | varchar(64) | Cron Expressions · 可空 |
| `last_trigger_time` | timestamp | Last Trigger Time · 可空 |
| `next_trigger_time` | timestamp | Next Trigger Time · 可空 |
| `except_holiday_flag` | char | Except Holiday Flag: Y/N |
| `enable_flag` | char | Enable Flag: Y/N |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`rule_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
