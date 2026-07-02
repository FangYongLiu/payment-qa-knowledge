---
id: tbl_marketgoods_t_goods_channel
object_type: Table
name: 商品渠道表 (t_goods_channel)
aliases: [t_goods_channel, marketgoods.t_goods_channel]
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

# 商品渠道表 (t_goods_channel)

## 用途
物理表 `marketgoods.t_goods_channel`,主键 `id`。商品渠道表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `goods_code` | varchar(16) | 商品编号 |
| `channel_code` | varchar(300) | 渠道code · 可空 |
| `sku_code` | varchar(16) | 商品sku编号 · 可空 |
| `supplier_no` | varchar(64) | 供应商编号 |
| `gmt_created` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- `idx_goods_code`:goods_code

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
