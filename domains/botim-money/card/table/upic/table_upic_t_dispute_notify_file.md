---
id: tbl_upic_t_dispute_notify_file
object_type: Table
name: 差错退款文件 (t_dispute_notify_file)
aliases: [t_dispute_notify_file, upic.t_dispute_notify_file]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: upic schema DDL
tags: [card, upic]
sensitivity: normal
related_services: []
---

# 差错退款文件 (t_dispute_notify_file)

## 用途
物理表 `upic.t_dispute_notify_file`,主键 `dispute_file_id`。差错退款文件。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `dispute_file_id` | int | 差错文件ID · 可空 |
| `file_tag` | varchar(90) | 文件tag |
| `handle_status` | char | 处理状态;初始I；处理成功S； |
| `file_name` | varchar(32) | dispute文件名 |
| `row_count` | int | 文件行数 · 可空 |
| `memo` | varchar(90) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`dispute_file_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
