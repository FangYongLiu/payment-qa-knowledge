---
id: tbl_payment_tb_party_payment_funds_05
object_type: Table
name: 参与方资金源 (tb_party_payment_funds_05)
aliases: [tb_party_payment_funds_05, payment.tb_party_payment_funds_05]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# 参与方资金源 (tb_party_payment_funds_05)

## 用途
物理表 `payment.tb_party_payment_funds_05`,主键 `PAYMENT_FUNDS_ID`。参与方资金源。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PAYMENT_FUNDS_ID` | decimal(18) | 机构收付信息ID，SEQ_INSTITUTION_PAYMENT_INFO |
| `PAYMENT_SEQ_NO` | varchar(32) | 支付流水号 |
| `PARTY_PAYMENT_ID` | decimal(18) | 会员支付信息ID，SEQ_MEMBER_PAYMENT_INFO |
| `TARGET_INST_CODE` | varchar(32) | 目标机构 · 可空 |
| `FUNDS_CHANNEL_CODE` | varchar(32) | 资金通道编码 · 可空 |
| `EXTENSION` | varchar(4000) | 扩展信息 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |

## 主键 / 索引
- 主键:`PAYMENT_FUNDS_ID`
- `IDX_PARTY_PAY_FUNDS_PPID_05`:PARTY_PAYMENT_ID
- `IDX_PARTY_PAY_FUNDS_PSN_05`:PAYMENT_SEQ_NO

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
