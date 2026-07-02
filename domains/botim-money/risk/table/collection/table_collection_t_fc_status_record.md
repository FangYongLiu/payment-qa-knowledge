---
id: tbl_collection_t_fc_status_record
object_type: Table
name: 用户状态记录表 (t_fc_status_record)
aliases: [t_fc_status_record, collection.t_fc_status_record]
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

# 用户状态记录表 (t_fc_status_record)

## 用途
物理表 `collection.t_fc_status_record`,主键 `id`。用户状态记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 主健 · 可空 |
| `create_by` | varchar(50) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `update_by` | varchar(50) | 修改人 · 可空 |
| `uid` | varchar(50) | uid |
| `user_uid` | varchar(50) | 用户id |
| `date` | date | 日期 |
| `available_time` | int(5) | 可用时长 |
| `busy_time` | int(5) | 繁忙时长 |
| `ptp_time` | int(5) | ptp时长 |
| `lunch_time` | int(5) | lunch时长 |
| `small_time` | int(5) | small时长 |
| `ptp_count` | int(5) | 当天ptp次数 |
| `stage_name` | varchar(10) | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_date`:date
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
