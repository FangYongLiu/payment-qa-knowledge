---
id: tbl_collection_col_order_collection
object_type: Table
name: 分案表 (col_order_collection)
aliases: [col_order_collection, collection.col_order_collection]
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

# 分案表 (col_order_collection)

## 用途
物理表 `collection.col_order_collection`,主键 `id`。分案表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(100) | 更新人员 · 可空 |
| `collection_level` | tinyint(5) | 催收等级 1催收员工 2 经理 |
| `create_type` | tinyint(5) | 方式 0 自动分配 1手动 |
| `create_uid` | varchar(64) | 分配者id · 可空 |
| `invalid_type` | tinyint(5) | 无效原因 · 可空 |
| `is_valid` | tinyint(5) | 是否最新 1当前 0已过期 |
| `last_user_uid` | varchar(64) | 上次催收员 · 可空 |
| `member_id` | varchar(64) | 债务人 |
| `order_collecton_uid` | varchar(64) | 分案id |
| `bill_no` | varchar(64) | 订单 |
| `user_uid` | varchar(64) | 催收员 |
| `stage_name` | varchar(64) | 所属帐龄名称 · 可空 |
| `config_key` | varchar(64) | 分案对应的属性值 · 可空 |
| `score` | decimal(11, 10) | 模型分数 · 可空 |
| `will_repay_capital` | decimal(19, 2) | 分案当时应还本金 · 可空 |
| `will_repay_fee` | decimal(19, 2) | 分案当时应还手续费 · 可空 |
| `will_repay_penalty` | decimal(19, 2) | 分案当时应还罚息 · 可空 |
| `already_repay_capital` | decimal(19, 2) | 分案当时已还本金 · 可空 |
| `already_repay_fee` | decimal(19, 2) | 分案当时已还手续费 · 可空 |
| `already_repay_penalty` | decimal(19, 2) | 分案当时已还利息 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_create_time`:create_time
- `idx_member_id`:member_id
- `idx_order_collecton_uid`:order_collecton_uid
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
