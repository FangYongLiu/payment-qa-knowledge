---
id: tbl_bill_t_product_tag
object_type: Table
name: 产品标签 (t_product_tag)
aliases: [t_product_tag, bill.t_product_tag]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bill schema DDL
tags: [payment-core, bill]
sensitivity: normal
related_services: []
---

# 产品标签 (t_product_tag)

## 用途
物理表 `bill.t_product_tag`,主键 `id`。产品标签。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `tag` | varchar(32) | 产品标签 |
| `host_app` | varchar(32) | hostapp partnerId · 可空 |
| `tag_icon` | varchar(255) | 产品标签图标 · 可空 |
| `tag_category` | varchar(32) | 名称表达式 · 可空 |
| `sort` | int | 顺序 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_tag_hostapp`:tag, host_app (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
