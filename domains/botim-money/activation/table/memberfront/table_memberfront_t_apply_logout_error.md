---
id: tbl_memberfront_t_apply_logout_error
object_type: Table
name: table for recording error of applying logout (t_apply_logout_error)
aliases: [t_apply_logout_error, memberfront.t_apply_logout_error]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: memberfront schema DDL
tags: [activation, memberfront]
sensitivity: normal
related_services: []
---

# table for recording error of applying logout (t_apply_logout_error)

## 用途
物理表 `memberfront.t_apply_logout_error`,主键 `id`。table for recording error of applying logout。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(32) | primary key |
| `member_id` | varchar(20) | member id |
| `flow_name` | varchar(32) | flow name |
| `result_code` | varchar(50) | error code · 可空 |
| `result_msg` | varchar(500) | error detail · 可空 |
| `stage` | varchar(32) | stage · 可空 |
| `extension` | varchar(255) | extension field · 可空 |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_memberid`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
