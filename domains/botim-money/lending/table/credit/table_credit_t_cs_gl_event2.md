---
id: tbl_credit_t_cs_gl_event2
object_type: Table
name: gl event record (t_cs_gl_event2)
aliases: [t_cs_gl_event2, credit.t_cs_gl_event2]
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

# gl event record (t_cs_gl_event2)

## 用途
物理表 `credit.t_cs_gl_event2`,主键 `id`。gl event record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `order_no` | varchar(64) | order_no |
| `bus_no` | varchar(64) | bus_no |
| `scenario` | varchar(64) | scenario |
| `bus_time` | timestamp | bus_time · 可空 |
| `detail` | varchar(255) | detail · 可空 |
| `status` | tinyint(5) | 待补 |
| `created_time` | timestamp | created time · 可空 |
| `last_modified` | timestamp | update time · 可空 |
| `flag` | smallint | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_unique_order_no`:order_no, bus_no, scenario (UNIQUE)
- `idx_bus_no`:bus_no
- `idx_bus_time`:bus_time, status
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
