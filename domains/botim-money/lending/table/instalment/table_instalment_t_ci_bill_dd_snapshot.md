---
id: tbl_instalment_t_ci_bill_dd_snapshot
object_type: Table
name: Bill 刚过due_time 时的snapshot (t_ci_bill_dd_snapshot)
aliases: [t_ci_bill_dd_snapshot, instalment.t_ci_bill_dd_snapshot]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: instalment schema DDL
tags: [lending, instalment]
sensitivity: normal
related_services: []
---

# Bill 刚过due_time 时的snapshot (t_ci_bill_dd_snapshot)

## 用途
物理表 `instalment.t_ci_bill_dd_snapshot`,主键 `id`。Bill 刚过due_time 时的snapshot。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `bill_id` | int | t_cs_bill表的id |
| `order_no` | varchar(64) | Bill所属订单no |
| `snapshot_date` | varchar(255) | due_time的日期 |
| `remain_repay_fee` | decimal(15, 2) | 已还利息 |
| `create_time` | timestamp | 创建日期 |

## 主键 / 索引
- 主键:`id`
- `uk_billid`:bill_id (UNIQUE)
- `ix_date`:snapshot_date

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
