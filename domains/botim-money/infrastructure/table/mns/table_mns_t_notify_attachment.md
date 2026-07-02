---
id: tbl_mns_t_notify_attachment
object_type: Table
name: 附件 (t_notify_attachment)
aliases: [t_notify_attachment, mns.t_notify_attachment]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mns schema DDL
tags: [infrastructure, mns]
sensitivity: normal
related_services: []
---

# 附件 (t_notify_attachment)

## 用途
物理表 `mns.t_notify_attachment`,主键 `id`。附件。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键id · 可空 |
| `msg_id` | bigint(18) | 关联t_notify_msg的id |
| `file_name` | varchar(255) | 文件名 |
| `ref_url` | varchar(2000) | 文件存储于某一系统中(ufs)的url |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `memo` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_msg_id`:msg_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
