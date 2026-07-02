---
id: tbl_collection_t_col_coupon
object_type: Table
name: 发放优惠券记录表 (t_col_coupon)
aliases: [t_col_coupon, collection.t_col_coupon]
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

# 发放优惠券记录表 (t_col_coupon)

## 用途
物理表 `collection.t_col_coupon`,主键 `id`。发放优惠券记录表。业务语义细节**待补**(表结构来自 DDL)。

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
| `update_time` | timestamp | 修改时间 · 可空 |
| `update_by` | varchar(100) | 修改人 · 可空 |
| `coupon_id` | bigint(10) | 优惠卷id |
| `user_uid` | varchar(50) | 员工号 |
| `member_id` | varchar(20) | 用户号 |
| `bill_no` | varchar(50) | 账单号 |
| `order_no` | varchar(50) | 订单号 |
| `coupon_amount` | decimal(10, 2) | 面值 · 可空 |
| `invalid_time` | timestamp | 失效时间 · 可空 |
| `type` | tinyint(5) | Type: 1=Repayment Penalty Coupon, 2=Deferral Coupon, 3=Extension Discount Coupon · 可空 |
| `status` | tinyint(5) | State 0: Initial 1: Use 9:No Coupon · 可空 |
| `repay_id` | varchar(40) | 还款id · 可空 |
| `approver` | varchar(64) | approver · 可空 |
| `approve_time` | datetime(3) | approval time · 可空 |
| `approve_status` | tinyint | 0 Pending review 1 Approved 2 Rejected |
| `discount_percentage` | smallint | Discount percentage 0-100 · 可空 |
| `justification` | varchar(255) | Maker justification text · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_create_time`:create_time
- `idx_order_no`:order_no
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
