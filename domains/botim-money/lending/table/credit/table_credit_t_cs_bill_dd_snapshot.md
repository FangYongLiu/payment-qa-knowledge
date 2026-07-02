---
id: tbl_credit_t_cs_bill_dd_snapshot
object_type: Table
name: Bill 刚过due_time 时的snapshot (t_cs_bill_dd_snapshot)
aliases: [t_cs_bill_dd_snapshot, credit.t_cs_bill_dd_snapshot]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# Bill 刚过due_time 时的snapshot (t_cs_bill_dd_snapshot)

## 用途
物理表 `credit.t_cs_bill_dd_snapshot`,主键 `id`。Bill 刚过due_time 时的snapshot。业务语义细节**待补**(表结构来自 DDL)。

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
| `snapshot_date` | char(8) | due_time的日期 |
| `remain_repay_fee` | decimal(15, 2) | 已还利息 |
| `create_time` | timestamp | 创建日期 |
| `status` | smallint | 处理状态：0 未处理，1：已处理 |

## 主键 / 索引
- 主键:`id`
- `uk_billid`:bill_id (UNIQUE)
- `ix_date`:snapshot_date, status

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
