---
id: tbl_collection_t_col_order_collection_exp
object_type: Table
name: order collection exp info (t_col_order_collection_exp)
aliases: [t_col_order_collection_exp, collection.t_col_order_collection_exp]
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

# order collection exp info (t_col_order_collection_exp)

## 用途
物理表 `collection.t_col_order_collection_exp`,主键 `id`。order collection exp info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 待补 · 可空 |
| `create_time` | timestamp | 待补 |
| `bill_no` | varchar(64) | bill_no |
| `order_collection_uid` | varchar(64) | collection_uid |
| `exp_group` | varchar(64) | exp_group |
| `exp_name` | varchar(64) | exp name |
| `exp_result` | varchar(64) | exp result |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `uk_collection_uid`:order_collection_uid, exp_group

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
