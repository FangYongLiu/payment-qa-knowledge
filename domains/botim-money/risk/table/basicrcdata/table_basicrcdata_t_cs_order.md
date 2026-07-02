---
id: tbl_basicrcdata_t_cs_order
object_type: Table
name: zfjs实例中credit库的订单表 (t_cs_order)
aliases: [t_cs_order, basicrcdata.t_cs_order]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basicrcdata schema DDL
tags: [risk, basicrcdata]
sensitivity: normal
related_services: []
---

# zfjs实例中credit库的订单表 (t_cs_order)

## 用途
物理表 `basicrcdata.t_cs_order`,主键 `id`。zfjs实例中credit库的订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `status` | int | 状态 |
| `loan_amount` | decimal(15, 2) | 借款金额 |
| `user_id` | varchar(50) | 用户ID |
| `credit_id` | int | 授信ID |
| `identity` | varchar(100) | 身份证 |
| `vendor` | varchar(50) | 放款资方 · 可空 |
| `period` | smallint (5) | 借款期限 |
| `period_unit` | smallint(5) | 期限单位：0 天 1 月 2年 |
| `loan_time` | timestamp | 放款时间 · 可空 |
| `rebate` | int(5) | 借款利率 |
| `penalty` | int(5) | 罚息利率 |
| `finish_repay_time` | timestamp | 实际还款时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `order_no` | varchar(64) | 订单唯一ID |
| `is_read` | smallint(2) | 状态已读未读 |
| `audit_start_time` | timestamp | 待补 · 可空 |
| `audit_finish_time` | timestamp | 待补 · 可空 |
| `fee` | decimal(15, 2) | 手续费 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_credit_id`:credit_id
- `idx_identity`:identity
- `idx_order_no`:order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
