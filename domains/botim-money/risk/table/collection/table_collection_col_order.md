---
id: tbl_collection_col_order
object_type: Table
name: 催收订单表 (col_order)
aliases: [col_order, collection.col_order]
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

# 催收订单表 (col_order)

## 用途
物理表 `collection.col_order`,主键 `id`。催收订单表。业务语义细节**待补**(表结构来自 DDL)。

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
| `bill_no` | varchar(64) | 账单号 |
| `address` | varchar(255) | 地址 · 可空 |
| `will_repay_capital` | decimal(19, 2) | 应还本金 · 可空 |
| `will_repay_fee` | decimal(19, 2) | 应还手续费 · 可空 |
| `will_repay_penalty` | decimal(19, 2) | Should repay penalty · 可空 |
| `already_repay_capital` | decimal(19, 2) | 已还本金 · 可空 |
| `already_repay_fee` | decimal(19, 2) | 已还手续费 · 可空 |
| `already_repay_penalty` | decimal(19, 2) | 已还利息 · 可空 |
| `total_credit_amount` | decimal(19) | 总额度 · 可空 |
| `credit_amount` | decimal(19, 2) | 授信额度 · 可空 |
| `credit_id` | varchar(100) | 授信id · 可空 |
| `due_time` | timestamp | 还款时间 |
| `email` | varchar(255) | email · 可空 |
| `identity` | varchar(100) | 身份证 |
| `income` | varchar(100) | 收入 · 可空 |
| `is_repay` | tinyint(5) | 是否有还款 0初始 1还款 |
| `is_valid` | tinyint(5) | 是否有效 0初始 1已催收 |
| `loan_amount` | decimal(19, 2) | 借款金额 |
| `loan_time` | timestamp | 借款时间 |
| `member_id` | varchar(50) | 会员ID |
| `occupation` | varchar(100) | 职业 · 可空 |
| `order_no` | varchar(64) | 订单 |
| `penalty` | int | 罚息 · 可空 |
| `period` | int | 期限 · 可空 |
| `phone` | varchar(100) | 电话 · 可空 |
| `rebate` | int | 利率 · 可空 |
| `source` | int | 业务来源 1cashnow |
| `statge` | int | 当前期数 |
| `status` | tinyint(5) | 状态 -1退款 0:初始 1待分配 2再分配 3在催 4完结  |
| `total_order_no` | varchar(64) | 总订单号 |
| `source_order_no` | varchar(64) | 展期源订单号 · 可空 |
| `total_statge` | int | 总期数 |
| `totok_id` | varchar(200) | totokid · 可空 |
| `name` | varchar(255) | 姓名 · 可空 |
| `due_time_amount` | decimal(19, 2) | 逾期时逾期本金 · 可空 |
| `finish_time` | timestamp | 结清时间 · 可空 |
| `last_repay_time` | timestamp | 最后一次还款时间 · 可空 |
| `finish_due_days` | int(4) | 完结时逾期天数 · 可空 |
| `times` | smallint(5) | 借款次数 · 可空 |
| `monthly` | int(5) | 月份 · 可空 |
| `product` | tinyint(5) | 产品 cashnow100 paylater200 |
| `is_extension` | tinyint(5) | 是否展期 · 可空 |
| `extension_times` | tinyint(5) | 展期次数 · 可空 |
| `finish_type` | tinyint(5) | 完结类型 1普通 2展期  · 可空 |
| `oper_system` | tinyint(5) | 借款时操作系统 1:android 2:ios · 可空 |
| `partner_id` | varchar(20) | 渠道 |
| `extra_content` | varchar(500) | Extra content from order MQ, stored as JSON · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_due_time`:due_time
- `idx_identity`:identity
- `idx_member_id`:member_id
- `idx_order_no`:order_no
- `idx_source_order_no`:source_order_no
- `idx_total_order_no`:total_order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
