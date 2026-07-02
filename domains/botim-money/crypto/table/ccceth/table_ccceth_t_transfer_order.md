---
id: tbl_ccceth_t_transfer_order
object_type: Table
name: 提现订单 (t_transfer_order)
aliases: [t_transfer_order, ccceth.t_transfer_order]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccceth schema DDL
tags: [crypto, ccceth]
sensitivity: normal
related_services: []
---

# 提现订单 (t_transfer_order)

## 用途
物理表 `ccceth.t_transfer_order`,主键 `id`。提现订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `payer_address` | varchar(200) | 付款地址 |
| `receiver_address` | varchar(200) | 收款地址 |
| `currency_code` | varchar(32) | 收款币种 |
| `amount` | decimal(23, 8) | 收款金额 |
| `cent_amount` | decimal(32) | 收款金额(分) |
| `tx_hash` | varchar(200) | 事务hash · 可空 |
| `estimate_gas` | varchar(50) | 预估邮费 · 可空 |
| `status` | varchar(32) | status |
| `fail_message` | varchar(128) | 错误原因 · 可空 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `include_fee` | varchar(32) | 转账费用包含在金额中 · 可空 |
| `actual_cent` | decimal(32) | 实际转账金额 · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_tso_ct`:created_time
- `i_tso_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
