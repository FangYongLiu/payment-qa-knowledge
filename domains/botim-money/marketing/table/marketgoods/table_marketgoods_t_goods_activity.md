---
id: tbl_marketgoods_t_goods_activity
object_type: Table
name: 商品活动表 (t_goods_activity)
aliases: [t_goods_activity, marketgoods.t_goods_activity]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketgoods schema DDL
tags: [marketing, marketgoods]
sensitivity: normal
related_services: []
---

# 商品活动表 (t_goods_activity)

## 用途
物理表 `marketgoods.t_goods_activity`,主键 `id`。商品活动表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `goods_code` | varchar(16) | 商品编号 |
| `sku_code` | varchar(150) | 商品SKU编号 · 可空 |
| `activity_code` | varchar(16) | 活动编号 |
| `join_type` | char | 加入类型（J:参与 C：可选择不参与） |
| `create_time` | timestamp | 创建时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
