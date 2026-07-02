---
id: tbl_ccwithdraw_t_withdraw_order
object_type: Table
name: 提现订单 (t_withdraw_order)
aliases: [t_withdraw_order, ccwithdraw.t_withdraw_order]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccwithdraw schema DDL
tags: [crypto, ccwithdraw]
sensitivity: normal
related_services: []
---

# 提现订单 (t_withdraw_order)

## 用途
物理表 `ccwithdraw.t_withdraw_order`,主键 `id`。提现订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `currency_code` | varchar(32) | 提币币种 |
| `amount` | decimal(23, 8) | 提币金额 |
| `actual_received_crcy` | varchar(32) | 实际到账币种 · 可空 |
| `actual_received_amt` | decimal(23, 8) | 实际到账金额 · 可空 |
| `actual_wtd_fee` | decimal(23, 8) | 实际手续费 · 可空 |
| `actual_wtd_fee_crcy` | varchar(32) | 实际手续费币种 · 可空 |
| `customer_mid` | varchar(32) | 用户MID |
| `merchant_mid` | varchar(32) | merchantMid |
| `network` | varchar(32) | 网络 |
| `memo` | varchar(128) | 备注 · 可空 |
| `txid` | varchar(128) | txid · 可空 |
| `address` | varchar(128) | 提币地址 |
| `expected_received_crcy` | varchar(32) | 预计到账币种 |
| `expected_received_amt` | decimal(23, 8) | 预计到账金额 |
| `expected_wtd_fee` | decimal(23, 8) | 预计手续费 |
| `expected_wtd_fee_crcy` | varchar(32) | 预计手续费币种 |
| `status` | varchar(32) | status |
| `gain_or_loss_crcy` | varchar(32) | 盈亏币种 · 可空 |
| `gain_or_loss_amt` | decimal(23, 8) | 盈亏金额 · 可空 |
| `fail_message` | varchar(128) | 错误原因 · 可空 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `platform_id` | varchar(32) | platformId · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_wo_ct`:created_time
- `i_wo_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
