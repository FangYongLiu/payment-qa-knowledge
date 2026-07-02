---
id: tbl_csc_tr_notify_define_group
object_type: Table
name: 通知定义和组关联 (tr_notify_define_group)
aliases: [tr_notify_define_group, csc.tr_notify_define_group]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: csc schema DDL
tags: [merchant-management, csc]
sensitivity: normal
related_services: []
---

# 通知定义和组关联 (tr_notify_define_group)

## 用途
物理表 `csc.tr_notify_define_group`,主键 `relate_id`。通知定义和组关联。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `relate_id` | bigint | 关联ID · 可空 |
| `define_type` | varchar(10) | 定义类型：C=对账，M=监控 |
| `define_id` | bigint | 定义ID |
| `group_id` | bigint | 组ID |
| `create_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`relate_id`
- `uk_define_group`:define_id, define_type, group_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
