---
id: tbl_supplier_leaf_alloc
object_type: Table
name: 订单号生成表 (leaf_alloc)
aliases: [leaf_alloc, supplier.leaf_alloc]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: supplier schema DDL
tags: [marketing, supplier]
sensitivity: normal
related_services: []
---

# 订单号生成表 (leaf_alloc)

## 用途
物理表 `supplier.leaf_alloc`,主键 `biz_tag`。订单号生成表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `biz_tag` | varchar(128) | sequence名称 |
| `max_id` | bigint | 当前序列最大值，亦即下次取值的初始值 |
| `step` | int | 初始情况下在内存中缓冲的序列号个数，一般配置表为10，订单表为200以上，看订单量 |
| `description` | varchar(255) | 描述 · 可空 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`biz_tag`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
