---
id: tbl_reconciliation_t_weekly_buiness_recon_report
object_type: Table
name: Weekly Buiness Recon Report (t_weekly_buiness_recon_report)
aliases: [t_weekly_buiness_recon_report, reconciliation.t_weekly_buiness_recon_report]
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

# Weekly Buiness Recon Report (t_weekly_buiness_recon_report)

## 用途
物理表 `reconciliation.t_weekly_buiness_recon_report`,主键 `id`。Weekly Buiness Recon Report。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID：eight before and nine after |
| `report_type` | varchar(32) | Report Type |
| `start_date` | date | Start Date |
| `end_date` | date | End Date |
| `unrecon_num` | int | Un Reconciliation Number · 可空 |
| `fail_num` | int | Recon Fail Num · 可空 |
| `fail_amount` | decimal(19, 4) | Recon Fail Amount · 可空 |
| `initial_num` | int | Fund Flow Initial Num · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(512) | Memo · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`id`
- `uk_type_date`:report_type, start_date, end_date (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
