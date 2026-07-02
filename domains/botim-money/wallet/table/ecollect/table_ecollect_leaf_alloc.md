---
id: tbl_ecollect_leaf_alloc
object_type: Table
name: Leaf allocation table for ID generation (leaf_alloc)
aliases: [leaf_alloc, ecollect.leaf_alloc]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ecollect schema DDL
tags: [wallet, ecollect]
sensitivity: normal
related_services: []
---

# Leaf allocation table for ID generation (leaf_alloc)

## 用途
物理表 `ecollect.leaf_alloc`,主键 `biz_tag`。Leaf allocation table for ID generation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `biz_tag` | varchar(128) | Sequence name |
| `max_id` | bigint | Current sequence max value |
| `step` | int | Number of sequence numbers buffered in memory |
| `description` | varchar(255) | Description · 可空 |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`biz_tag`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
