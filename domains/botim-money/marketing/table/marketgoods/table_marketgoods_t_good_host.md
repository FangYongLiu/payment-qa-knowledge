---
id: tbl_marketgoods_t_good_host
object_type: Table
name: 商品与宿主表 (t_good_host)
aliases: [t_good_host, marketgoods.t_good_host]
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

# 商品与宿主表 (t_good_host)

## 用途
物理表 `marketgoods.t_good_host`,主键 `id`。商品与宿主表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `goods_code` | varchar(100) | 商品code · 可空 |
| `host_app` | varchar(100) | 平台：totok，payby，botim · 可空 |
| `status` | tinyint(3) | 状态（0：下架 1：上架 ） |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
