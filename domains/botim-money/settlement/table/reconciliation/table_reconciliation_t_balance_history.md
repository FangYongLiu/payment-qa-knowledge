---
id: tbl_reconciliation_t_balance_history
object_type: Table
name: Balance History Table (t_balance_history)
aliases: [t_balance_history, reconciliation.t_balance_history]
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

# Balance History Table (t_balance_history)

## 用途
物理表 `reconciliation.t_balance_history`,主键 `version_id`。Balance History Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `version_id` | bigint | Version Id：Eight before and nine after |
| `monitor_id` | int | Monitor ID |
| `balance` | decimal(19, 4) | Balance · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(512) | Memo · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`version_id`
- `idx_monitorId`:monitor_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
