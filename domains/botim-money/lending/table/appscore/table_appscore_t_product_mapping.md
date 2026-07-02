---
id: tbl_appscore_t_product_mapping
object_type: Table
name: 产品映射表 (t_product_mapping)
aliases: [t_product_mapping, appscore.t_product_mapping]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: appscore schema DDL
tags: [lending, appscore]
sensitivity: normal
related_services: []
---

# 产品映射表 (t_product_mapping)

## 用途
物理表 `appscore.t_product_mapping`,主键 `biz_product_code`。产品映射表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `biz_product_code` | varchar(10) | 产品编码 |
| `name` | varchar(20) | 产品名称 |
| `cleaning_code` | varchar(20) | 清算编码 |

## 主键 / 索引
- 主键:`biz_product_code`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
