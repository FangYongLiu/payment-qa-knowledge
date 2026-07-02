---
id: tbl_mchtsettle_t_stmt_event2
object_type: Table
name: statement event2 (t_stmt_event2)
aliases: [t_stmt_event2, mchtsettle.t_stmt_event2]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, mchtsettle]
sensitivity: normal
related_services: []
---

# statement event2 (t_stmt_event2)

## 用途
物理表 `mchtsettle.t_stmt_event2`,主键 `id`。statement event2。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | evnet id |
| `order_id` | bigint | object id |
| `job_id` | bigint | job_id id |
| `created_time` | timestamp(3) | created_time |

## 主键 / 索引
- 主键:`id`
- `i_evt_ct`:created_time
- `i_evt_job`:job_id
- `i_evt_order`:order_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
