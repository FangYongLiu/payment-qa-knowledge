---
id: tbl_counter_t_bank_flow
object_type: Table
name: 银行流水表 (t_bank_flow)
aliases: [t_bank_flow, counter.t_bank_flow]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 银行流水表 (t_bank_flow)

## 用途
物理表 `counter.t_bank_flow`,主键 `flow_id`。银行流水表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 流水id |
| `bank_flow_id` | varchar(64) | 银行流水id · 可空 |
| `payer_name` | varchar(255) | 付款人名称 |
| `payer_account_no` | varchar(32) | 付款人账号编号 |
| `amount` | decimal(15, 2) | 金额 |
| `currency` | varchar(3) | 币种 |
| `status` | varchar(5) | 状态: I-初始、S-登账成功、F-登账失败 |
| `bank_date` | timestamp | 银行转账日期 · 可空 |
| `bank_code` | varchar(32) | 银行编码 |
| `account_id` | varchar(17) | 账户id · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `flow_type` | varchar(4) | 线下入金、PayRoll · 可空 |
| `batch_id` | bigint(17) | 批次id · 可空 |
| `gmt_start` | timestamp | 起始日期 · 可空 |
| `gmt_end` | timestamp | 结束日期 · 可空 |
| `payer_name_ticket` | varchar(32) | 收款人名称标志 · 可空 |
| `days` | int | 日期 · 可空 |
| `bill_memo` | varchar(256) | 通知账单内容 · 可空 |
| `offline_deposit_type` | varchar(8) | 入金类型 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- `uk_flow_bank_status`:bank_flow_id, bank_code, status (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
