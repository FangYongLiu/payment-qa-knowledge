---
id: tbl_ccwithdraw_t_channel_withdraw_order
object_type: Table
name: 渠道提现订单 (t_channel_withdraw_order)
aliases: [t_channel_withdraw_order, ccwithdraw.t_channel_withdraw_order]
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

# 渠道提现订单 (t_channel_withdraw_order)

## 用途
物理表 `ccwithdraw.t_channel_withdraw_order`,主键 `id`。渠道提现订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `apply_amount_crcy` | varchar(32) | 币种 |
| `apply_amount` | decimal(23, 8) | 金额 |
| `txid` | varchar(128) | txid · 可空 |
| `merchant_mid` | varchar(32) | merchantMid |
| `received_crcy` | varchar(32) | 到账币种 · 可空 |
| `received_amt` | decimal(23, 8) | 到账金额 · 可空 |
| `network` | varchar(32) | 网络 |
| `address` | varchar(128) | 提币地址 |
| `withdraw_fee_crcy` | varchar(32) | 手续费币种 · 可空 |
| `withdraw_fee` | decimal(23, 8) | 手续费金额 · 可空 |
| `supplier_order_id` | varchar(64) | 供应商订单号 · 可空 |
| `apply_time` | timestamp(3) | 申请时间 · 可空 |
| `operator_mid` | varchar(64) | 操作员ID · 可空 |
| `expired_time` | timestamp(3) | 超时时间 |
| `status` | varchar(32) | status |
| `fail_message` | varchar(128) | 错误原因 · 可空 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `i_cwo_ct`:created_time
- `i_cwo_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
