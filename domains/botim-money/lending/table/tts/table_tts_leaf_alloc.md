---
id: tbl_tts_leaf_alloc
object_type: Table
name: sequence cache table (leaf_alloc)
aliases: [leaf_alloc, tts.leaf_alloc]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: tts schema DDL
tags: [lending, tts]
sensitivity: normal
related_services: []
---

# sequence cache table (leaf_alloc)

## 用途
物理表 `tts.leaf_alloc`,主键 `biz_tag`。sequence cache table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `biz_tag` | varchar(128) | sequence name |
| `max_id` | bigint | max value for sequecne |
| `step` | int | cache num，normally 10，order table 200,depends on the trans volume |
| `description` | varchar(255) | description · 可空 |
| `update_time` | timestamp(3) | update time |

## 主键 / 索引
- 主键:`biz_tag`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
