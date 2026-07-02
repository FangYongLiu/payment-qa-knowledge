---
id: tbl_transfer_t_split_party
object_type: Table
name: 分账信息扩展 (t_split_party)
aliases: [t_split_party, transfer.t_split_party]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: transfer schema DDL
tags: [wallet, transfer]
sensitivity: normal
related_services: []
---

# 分账信息扩展 (t_split_party)

## 用途
物理表 `transfer.t_split_party`,主键 `split_id`。分账信息扩展。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `split_id` | bigint(17) | 分账信息id |
| `settle_no` | bigint(18) | 结算凭证号 |
| `split_tag` | varchar(16) | 分账类型 · 可空 |
| `amount` | decimal(15, 4) | 金额 |
| `currency` | varchar(10) | 币种 |
| `payer_id` | varchar(32) | 付款方客户id |
| `payer_account_no` | varchar(32) | 付款方账户 |
| `payer_identity` | varchar(32) | 付款方标识 · 可空 |
| `payer_identity_type` | varchar(16) | 付款方标识类型 · 可空 |
| `payer_account_type` | varchar(16) | 付款方账户类型 · 可空 |
| `payee_id` | varchar(32) | 收款方客户id |
| `payee_account_no` | varchar(32) | 收款方账户 |
| `payee_identity` | varchar(32) | 收款方标识 · 可空 |
| `payee_identity_type` | varchar(16) | 收款方标识类型 · 可空 |
| `payee_account_type` | varchar(16) | 收款方账户类型 · 可空 |
| `memo` | varchar(256) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`split_id`
- `idx_split_party_payee_id`:payee_id
- `idx_split_party_payer_id`:payer_id
- `idx_split_party_settle_no`:settle_no

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
