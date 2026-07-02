---
id: tbl_counter_tb_sys_notice
object_type: Table
name: 通知表 (tb_sys_notice)
aliases: [tb_sys_notice, counter.tb_sys_notice]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 通知表 (tb_sys_notice)

## 用途
物理表 `counter.tb_sys_notice`,主键 `notice_id`。通知表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `notice_id` | bigint | 主键 |
| `title` | varchar(255) | 标题 · 可空 |
| `content` | text | 内容 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `create_user` | bigint | 创建人 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `update_user` | bigint | 修改人 · 可空 |

## 主键 / 索引
- 主键:`notice_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
