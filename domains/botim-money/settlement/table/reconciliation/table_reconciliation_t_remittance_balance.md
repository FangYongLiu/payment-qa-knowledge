---
id: tbl_reconciliation_t_remittance_balance
object_type: Table
name: 汇款渠道余额对账表 (t_remittance_balance)
aliases: [t_remittance_balance, reconciliation.t_remittance_balance]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 汇款渠道余额对账表 (t_remittance_balance)

## 用途
物理表 `reconciliation.t_remittance_balance`,主键 `id`。汇款渠道余额对账表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id 前八后九 |
| `channel_code` | varchar(16) | 渠道代码 |
| `account_type` | varchar(4) | 账户类型 USDT/USD/CNY/INR等 |
| `bill_date` | char(8) | 对账日期 |
| `beginning_amount` | decimal(19, 4) | 日初金额 · 可空 |
| `merchant_change_amount` | decimal(19, 4) | 商户控台变动金额 · 可空 |
| `operating_exchange_amount` | decimal(19, 4) | 运营控台变动金额 · 可空 |
| `fundout_amount` | decimal(19, 4) | 出款金额 · 可空 |
| `refund_amount` | decimal(19, 4) | 退款金额 · 可空 |
| `fee_amount` | decimal(19, 4) | 手续费金额 · 可空 |
| `inner_balance` | decimal(19, 4) | 内部日终余额 · 可空 |
| `outer_balance` | decimal(19, 4) | 外部日终余额 · 可空 |
| `difference_amount` | decimal(19, 4) | 差异金额 · 可空 |
| `currency` | varchar(4) | 币种 |
| `status` | char | 对账状态 I:初始化 S:成功 F:失败 |
| `adjust_status` | char | 调节状态 A:已调节 M:已修改金额 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_billDate_channelCode_accountType`:bill_date, channel_code, account_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
