---
id: tbl_pns_leaf_alloc
object_type: Table
name: 当前序列最大值，亦即下次取值的初始值 (leaf_alloc)
aliases: [leaf_alloc, pns.leaf_alloc]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pns schema DDL
tags: [infrastructure, pns]
sensitivity: normal
related_services: []
---

# 当前序列最大值，亦即下次取值的初始值 (leaf_alloc)

## 用途
物理表 `pns.leaf_alloc`,主键 `None`。当前序列最大值，亦即下次取值的初始值。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `biz_tag` | varchar | 待补 · 可空 |

## 主键 / 索引
- 主键:`None`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
