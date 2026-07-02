---
id: tbl_collection_t_col_remind_send_log
object_type: Table
name: remind send log table (t_col_remind_send_log)
aliases: [t_col_remind_send_log, collection.t_col_remind_send_log]
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

# remind send log table (t_col_remind_send_log)

## 用途
物理表 `collection.t_col_remind_send_log`,主键 `id`。remind send log table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `create_time` | timestamp | create_time · 可空 |
| `order_no` | varchar(40) | orderNo |
| `member_id` | varchar(20) | memberId |
| `due_time` | timestamp | duetime |
| `type` | tinyint(2) | 6:botim |
| `days` | int(4) | due_days |
| `template_uid` | varchar(50) | template_uid · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time
- `idx_member_id`:member_id
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
