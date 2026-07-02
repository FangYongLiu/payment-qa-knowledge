---
id: tbl_collection_t_col_template
object_type: Table
name: 模版表 (t_col_template)
aliases: [t_col_template, collection.t_col_template]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 模版表 (t_col_template)

## 用途
物理表 `collection.t_col_template`,主键 `id`。模版表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `update_by` | varchar(100) | 更新者 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `uid` | varchar(50) | uid |
| `enabled` | int(4) | 是否启用 |
| `content` | varchar(500) | 待补 · 可空 |
| `type` | int(4) | 类型 1短信 2邮件 3totok · 可空 |
| `start_days` | int(4) | 逾期起始时间 · 可空 |
| `end_days` | int(4) | 逾期结束时间 · 可空 |
| `param` | varchar(255) | 通配符参数 · 可空 |
| `join_id` | varchar(50) | 关联外部模版id · 可空 |
| `title` | varchar(50) | 模版标题 |
| `target_type` | tinyint | 目标类型0本人 1紧急联系人 · 可空 |
| `product` | tinyint(5) | 产品码 等同col_order/t_col_bill表product |

## 主键 / 索引
- 主键:`id`
- `idx_uid`:uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
