---
id: tbl_ecollect_t_product_stats
object_type: Table
name: Product aggregate stats (purchase + view counters) (t_product_stats)
aliases: [t_product_stats, ecollect.t_product_stats]
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

# Product aggregate stats (purchase + view counters) (t_product_stats)

## 用途
物理表 `ecollect.t_product_stats`,主键 `product_id`。Product aggregate stats (purchase + view counters)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `product_id` | bigint(21) | Product ID |
| `purchase_count` | bigint | Cumulative purchased quantity |
| `view_count` | bigint | Cumulative product detail views |
| `last_purchased_at` | timestamp | Last purchase time · 可空 |
| `last_viewed_at` | timestamp | Last view time · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time · 可空 |

## 主键 / 索引
- 主键:`product_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
