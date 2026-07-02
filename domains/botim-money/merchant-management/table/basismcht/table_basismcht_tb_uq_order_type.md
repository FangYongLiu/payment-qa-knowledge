---
id: tbl_basismcht_tb_uq_order_type
object_type: Table
name: 联合查询订单类型 (tb_uq_order_type)
aliases: [tb_uq_order_type, basismcht.tb_uq_order_type]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basismcht schema DDL
tags: [merchant-management, basismcht]
sensitivity: normal
related_services: []
---

# 联合查询订单类型 (tb_uq_order_type)

## 用途
物理表 `basismcht.tb_uq_order_type`,主键 `code`。联合查询订单类型。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `code` | varchar(32) | 代码 |
| `name` | varchar(64) | 名称 |
| `memo` | varchar(128) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`code`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
