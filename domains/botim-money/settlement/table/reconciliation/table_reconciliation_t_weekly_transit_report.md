---
id: tbl_reconciliation_t_weekly_transit_report
object_type: Table
name: Weekly Transit Report (t_weekly_transit_report)
aliases: [t_weekly_transit_report, reconciliation.t_weekly_transit_report]
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

# Weekly Transit Report (t_weekly_transit_report)

## 用途
物理表 `reconciliation.t_weekly_transit_report`,主键 `id`。Weekly Transit Report。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID：eight before and nine after |
| `fund_channel_code` | varchar(32) | Fund Channel Code |
| `execute_date` | date | Execute Date |
| `lack_date` | date | Lack Date |
| `latest_date` | date | Lastest Date · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(512) | Memo · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`id`
- `uk_type_date`:fund_channel_code, lack_date (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
