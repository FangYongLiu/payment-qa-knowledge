---
id: tbl_collection_t_col_reserve_record
object_type: Table
name: 留案记录表 (t_col_reserve_record)
aliases: [t_col_reserve_record, collection.t_col_reserve_record]
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

# 留案记录表 (t_col_reserve_record)

## 用途
物理表 `collection.t_col_reserve_record`,主键 `id`。留案记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 主健 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `bill_no` | varchar(64) | 账单号 |
| `member_id` | varchar(20) | 用户id |
| `collection_uid` | varchar(64) | 生成记录时对应的分案uid |
| `user_uid` | varchar(64) | 生成记录时对应的员工uid |
| `valid_start_time` | timestamp | 触发开始时间 · 可空 |
| `valid_end_time` | timestamp | 触发结束时间 · 可空 |
| `start_time` | timestamp | 留案开始时间 · 可空 |
| `end_time` | timestamp | 留案结束时间 · 可空 |
| `round` | tinyint(5) | 第几轮次 |
| `status` | tinyint(5) | 状态 -1:留案失败 0：初始 1：留案中 2：留案结束 |
| `repay_no` | varchar(40) | 成功触发留案的还款号 对应还款表repay_id · 可空 |
| `coupon_id` | bigint(10) | 留案成功时对应营销系统优惠卷id · 可空 |
| `will_repay_capital` | decimal(19, 2) | 应还本金 · 可空 |
| `will_repay_fee` | decimal(19, 2) | 应还手续费 · 可空 |
| `will_repay_penalty` | decimal(19, 2) | 应还罚息 · 可空 |
| `already_repay_capital` | decimal(19, 2) | 已还本金 · 可空 |
| `already_repay_fee` | decimal(19, 2) | 已还手续费 · 可空 |
| `already_repay_penalty` | decimal(19, 2) | 已还利息 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_collection_uid`:collection_uid
- `idx_end_time`:end_time
- `idx_member_id`:member_id
- `idx_start_time`:start_time
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
