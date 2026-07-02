---
id: tbl_collection_t_col_enable_expand_record
object_type: Table
name: 催收操作给用户展示展期入口记录表 (t_col_enable_expand_record)
aliases: [t_col_enable_expand_record, collection.t_col_enable_expand_record]
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

# 催收操作给用户展示展期入口记录表 (t_col_enable_expand_record)

## 用途
物理表 `collection.t_col_enable_expand_record`,主键 `id`。催收操作给用户展示展期入口记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `member_id` | varchar(20) | 用户id |
| `order_no` | varchar(64) | 对应col_order表中的order_no  |
| `expire_time` | timestamp | 开放时效截止时间  |
| `overdue_days_when_enable` | smallint(5) | 开放时，orderNo逾期天数  |
| `status` | smallint(4) | 状态：初始0  过期-1 展期或者结清1 |
| `operator_uid` | varchar(64) | 用户id |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time
- `idx_member_id`:member_id
- `idx_operator_uid`:operator_uid
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
