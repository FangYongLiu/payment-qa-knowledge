---
id: tbl_mns_t_msg_extension
object_type: Table
name: 消息扩展信息 (t_msg_extension)
aliases: [t_msg_extension, mns.t_msg_extension]
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

# 消息扩展信息 (t_msg_extension)

## 用途
物理表 `mns.t_msg_extension`,主键 `id`。消息扩展信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键id |
| `msg_id` | bigint(18) | 消息id |
| `ext_info` | varchar(2000) | 扩展信息 · 可空 |
| `gmt_modified` | timestamp | 修改时间 |
| `gmt_create` | timestamp | 创建时间 |
| `memo` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_msg_extension_msg_id`:msg_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
