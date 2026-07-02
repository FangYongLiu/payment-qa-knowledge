---
id: tbl_collection_t_col_botim_receive
object_type: Table
name: botim消息记录 (t_col_botim_receive)
aliases: [t_col_botim_receive, collection.t_col_botim_receive]
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

# botim消息记录 (t_col_botim_receive)

## 用途
物理表 `collection.t_col_botim_receive`,主键 `id`。botim消息记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `create_time` | timestamp | 待补 · 可空 |
| `update_time` | timestamp | 待补 · 可空 |
| `uid` | varchar(36) | uid · 可空 |
| `member_id` | varchar(20) | memberId |
| `order_no` | varchar(40) | orderNo |
| `bill_no` | varchar(40) | billNo · 可空 |
| `type` | tinyint(2) | 1、need_help 2、repay · 可空 |
| `collect_type` | tinyint(2) | 1cs 2user · 可空 |
| `user_uid` | varchar(36) | user_uid |
| `status` | tinyint(2) | 0初始 1解决 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_member_id`:member_id
- `idx_order_no`:order_no
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
