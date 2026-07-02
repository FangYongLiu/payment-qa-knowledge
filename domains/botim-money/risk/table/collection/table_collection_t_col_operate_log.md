---
id: tbl_collection_t_col_operate_log
object_type: Table
name: t_col_operate_log (t_col_operate_log)
aliases: [t_col_operate_log, collection.t_col_operate_log]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# t_col_operate_log (t_col_operate_log)

## 用途
物理表 `collection.t_col_operate_log`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `update_by` | varchar(100) | 修改人 · 可空 |
| `uid` | varchar(64) | 操作人 |
| `order_no` | varchar(64) | 订单 |
| `type` | int(4) | 类型 |
| `param` | varchar(500) | 参数 · 可空 |
| `reason_note` | varchar(100) | loan.update reasonNote (audit only) · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
