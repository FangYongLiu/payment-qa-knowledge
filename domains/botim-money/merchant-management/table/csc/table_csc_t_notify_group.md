---
id: tbl_csc_t_notify_group
object_type: Table
name: 通知组 (t_notify_group)
aliases: [t_notify_group, csc.t_notify_group]
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

# 通知组 (t_notify_group)

## 用途
物理表 `csc.t_notify_group`,主键 `group_id`。通知组。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `group_id` | bigint | 组ID · 可空 |
| `group_name` | varchar(128) | 组名称 |
| `is_main` | char | 是否主通知 Y:是 N:否 · 可空 |
| `teams_url` | varchar(512) | teams频道url · 可空 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`group_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
