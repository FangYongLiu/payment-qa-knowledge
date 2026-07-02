---
id: tbl_blackcredit_t_exit_order
object_type: Table
name: 离场订单 (t_exit_order)
aliases: [t_exit_order, blackcredit.t_exit_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: blackcredit schema DDL
tags: [lending, blackcredit]
sensitivity: normal
related_services: []
---

# 离场订单 (t_exit_order)

## 用途
物理表 `blackcredit.t_exit_order`,主键 `id`。离场订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 全局号 |
| `agency_mid` | varchar(32) | 代理人mid · 可空 |
| `player_mid` | varchar(32) | 玩家mid |
| `withdraw_amount` | decimal(19, 4) | 提现金额 |
| `withdraw_cur_code` | varchar(8) | 提现金额 |
| `qtn_snapshot_id` | bigint | 汇率报价快照id · 可空 |
| `fundout_amount` | decimal(19, 4) | 打款金额 · 可空 |
| `fundout_cur_code` | varchar(8) | 打款币种 · 可空 |
| `repay_amount` | decimal(19, 4) | 还款金额 · 可空 |
| `repay_cur_code` | varchar(8) | 还款币种 · 可空 |
| `expect_repay_amount` | decimal(19, 4) | 预期还款金额 · 可空 |
| `expect_repay_cur_code` | varchar(8) | 预期还款币种 · 可空 |
| `status` | varchar(32) | 收单状态 |
| `unity_result_code` | varchar(100) | 统一结果码 · 可空 |
| `fail_code` | varchar(50) | 错误码 · 可空 |
| `fail_message` | varchar(100) | 错误描述 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `i_ao_ct`:created_time
- `i_ao_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
