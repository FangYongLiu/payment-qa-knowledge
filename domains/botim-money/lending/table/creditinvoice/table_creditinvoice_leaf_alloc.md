---
id: tbl_creditinvoice_leaf_alloc
object_type: Table
name: leaf_alloc (leaf_alloc)
aliases: [leaf_alloc, creditinvoice.leaf_alloc]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: creditinvoice schema DDL
tags: [lending, creditinvoice]
sensitivity: normal
related_services: []
---

# leaf_alloc (leaf_alloc)

## 用途
物理表 `creditinvoice.leaf_alloc`,主键 `biz_tag`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `biz_tag` | varchar(128) | sequence名称 |
| `max_id` | bigint | 当前序列最大值 |
| `step` | int | 缓存的个数，一般配置表为10，订单表为200以上，看订单量 |
| `description` | varchar(256) | 描述 · 可空 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`biz_tag`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
