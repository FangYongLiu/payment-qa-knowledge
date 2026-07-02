---
id: tbl_credit_t_cs_extra_save_data
object_type: Table
name: Abnormal data recording (t_cs_extra_save_data)
aliases: [t_cs_extra_save_data, credit.t_cs_extra_save_data]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# Abnormal data recording (t_cs_extra_save_data)

## 用途
物理表 `credit.t_cs_extra_save_data`,主键 `id`。Abnormal data recording。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | id · 可空 |
| `created_time` | timestamp | create time |
| `last_modified` | timestamp | update time |
| `order_no` | varchar(100) | payment account |
| `status` | tinyint(5) | 0:init 1:finish |
| `type` | tinyint(5) | 1:buyback |
| `event_time` | timestamp | payment time |
| `json_data` | text | Json Data |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
