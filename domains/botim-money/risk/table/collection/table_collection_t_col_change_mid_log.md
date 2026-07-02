---
id: tbl_collection_t_col_change_mid_log
object_type: Table
name: change_mid_log (t_col_change_mid_log)
aliases: [t_col_change_mid_log, collection.t_col_change_mid_log]
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

# change_mid_log (t_col_change_mid_log)

## 用途
物理表 `collection.t_col_change_mid_log`,主键 `id`。change_mid_log。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | 待补 · 可空 |
| `request_no` | varchar(64) | request_no |
| `product` | smallint(4) | 待补 |
| `biz_bill_no` | varchar(64) | bill_no from snpl or easycash or other business |
| `old_member_id` | varchar(20) | old_member_id |
| `new_member_id` | varchar(20) | new_member_id |
| `snapshot_info` | varchar(1024) | snapshot_info · 可空 |
| `created_time` | timestamp | created_time |

## 主键 / 索引
- 主键:`id`
- `uk_rqn_p_bizno`:request_no, product, biz_bill_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
