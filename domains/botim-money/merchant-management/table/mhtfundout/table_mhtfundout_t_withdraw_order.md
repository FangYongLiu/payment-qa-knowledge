---
id: tbl_mhtfundout_t_withdraw_order
object_type: Table
name: 提现订单 (t_withdraw_order)
aliases: [t_withdraw_order, mhtfundout.t_withdraw_order]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mhtfundout schema DDL
tags: [merchant-management, mhtfundout]
sensitivity: normal
related_services: []
---

# 提现订单 (t_withdraw_order)

## 用途
物理表 `mhtfundout.t_withdraw_order`,主键 `global_id`。提现订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `request_no` | varchar(200) | 商户订单号 · 可空 |
| `order_usage` | varchar(50) | 用途 |
| `partner_id` | varchar(50) | 发起方memberId |
| `target_currency` | varchar(50) | 目标币种 |
| `bankcard_id` | varchar(50) | 绑卡id |
| `request_time` | timestamp(3) | 商户声明请求时间 |
| `currency` | varchar(50) | 提现币种 |
| `amount` | decimal(19, 4) | 提现金额 |
| `fee_currency` | varchar(50) | 费用币种 · 可空 |
| `fee_amount` | decimal(19, 4) | 费用金额 · 可空 |
| `receipt_currency` | varchar(50) | 到帐币种 · 可空 |
| `receipt_amount` | decimal(19, 4) | 到帐金额 · 可空 |
| `status` | varchar(50) | 状态 |
| `success_time` | timestamp(3) | 订单成功时间 · 可空 |
| `fail_code` | varchar(50) | 错误码 · 可空 |
| `fail_message` | varchar(200) | 错误描述 · 可空 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `type` | varchar(50) | 类型 · 可空 |
| `refunded_currency` | char(3) | 退款币种 · 可空 |
| `refunded_amount` | decimal(19, 4) | 退款金额 · 可空 |
| `creator_mid` | varchar(50) | 创建人MID · 可空 |
| `bank_reference` | varchar(128) | 银行关联号 · 可空 |
| `intermediate_account` | varchar(20) | intermediate account · 可空 |

## 主键 / 索引
- 主键:`global_id`
- `i_wo_ct`:created_time
- `i_wo_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
