---
id: tbl_basisportal_leaf_alloc
object_type: Table
name: leaf allocation table (leaf_alloc)
aliases: [leaf_alloc, basisportal.leaf_alloc]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basisportal schema DDL
tags: [merchant-management, basisportal]
sensitivity: normal
related_services: []
---

# leaf allocation table (leaf_alloc)

## 用途
物理表 `basisportal.leaf_alloc`,主键 `biz_tag`。leaf allocation table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `biz_tag` | varchar(128) | sequence name |
| `max_id` | bigint | current sequence max value,the initial value for the next retrieval |
| `step` | int | the number of sequence numbers buffered in memory under initial conditions |
| `description` | varchar(255) | description · 可空 |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`biz_tag`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
