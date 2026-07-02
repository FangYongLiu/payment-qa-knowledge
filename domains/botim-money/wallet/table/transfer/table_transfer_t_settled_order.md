---
id: tbl_transfer_t_settled_order
object_type: Table
name: 扩展参数 (t_settled_order)
aliases: [t_settled_order, transfer.t_settled_order]
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

# 扩展参数 (t_settled_order)

## 用途
物理表 `transfer.t_settled_order`,主键 `settle_no`。扩展参数。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `settle_no` | bigint(18) | 主键 · 可空 |
| `settle_trade_no` | bigint | 结算交易号 · 可空 |
| `payment_no` | bigint(18) | 付款订单号 |
| `out_settle_no` | varchar(64) | 商户结算订单 |
| `biz_product_code` | varchar(15) | 业务产品码 |
| `payee_uid` | varchar(32) | 收款人Uid |
| `payee_mid` | varchar(32) | 收款人memberId |
| `external_identity` | varchar(32) | 外部用户标示 · 可空 |
| `external_identity_type` | varchar(15) | 外部标示类型 · 可空 |
| `partner_id` | varchar(32) | 商户号 |
| `status` | varchar(20) | 状态 |
| `amount` | decimal(15, 4) | 金额 |
| `currency` | varchar(10) | 币种 |
| `settle_info` | varchar(100) | 结算信息，收款方式Json |
| `settle_type` | varchar(10) | 结算类型，ACCOUNT,CARD |
| `extend_info` | varchar | 待补 · 可空 |

## 主键 / 索引
- 主键:`settle_no`
- `idx_gmt_modified`:gmt_modified
- `idx_payment_no`:payment_no
- `idx_settle_trade_no`:settle_trade_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
