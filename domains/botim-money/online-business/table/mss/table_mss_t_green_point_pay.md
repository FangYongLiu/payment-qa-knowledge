---
id: tbl_mss_t_green_point_pay
object_type: Table
name: 积分发放支付表 (t_green_point_pay)
aliases: [t_green_point_pay, mss.t_green_point_pay]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 积分发放支付表 (t_green_point_pay)

## 用途
物理表 `mss.t_green_point_pay`,主键 `id`。积分发放支付表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `order_no` | varchar(32) | 积分服务记录订单号 |
| `pay_order` | varchar(32) | 积分服务记录支付订单号 |
| `pay_amount` | int | 奖励支付金额 |
| `pay_type` | varchar(32) | 奖励支付类型 · 可空 |
| `pay_sub_type` | varchar(32) | 奖励支付子类型 · 可空 |
| `status` | varchar(32) | 支付状态 |
| `member_id` | varchar(32) | 用户支付端会员号 · 可空 |
| `account_no` | varchar(32) | 支付账户 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
