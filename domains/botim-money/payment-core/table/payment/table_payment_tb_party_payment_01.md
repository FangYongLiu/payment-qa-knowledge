---
id: tbl_payment_tb_party_payment_01
object_type: Table
name: tb_party_payment_01 (tb_party_payment_01)
aliases: [tb_party_payment_01, payment.tb_party_payment_01]
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

# tb_party_payment_01 (tb_party_payment_01)

## 用途
物理表 `payment.tb_party_payment_01`,主键 `PAYMENT_PARTY_ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PAYMENT_PARTY_ID` | decimal(18) | 会员支付信息ID，SEQ_MEMBER_PAYMENT_INFO |
| `PAYMENT_SEQ_NO` | varchar(32) | YYYYMMDD||CODE[2]||SEQ_PAYMENT_ORDER[8] |
| `PARTY_ID_TYPE` | varchar(10) | 01 现金账户/废除不用 |
| `PARTY_ID` | varchar(64) | 会员标识，来源于帐户体系 |
| `ACCOUNT_NO` | varchar(32) | 账号 · 可空 |
| `FUND_PROP_TYPE` | char(2) | 待补 · 可空 |

## 主键 / 索引
- 主键:`PAYMENT_PARTY_ID`
- `IDX_PARTY_PAYMENT_PARTY_ID_01`:PARTY_ID
- `IDX_PARTY_PAYMENT_PSN_01`:PAYMENT_SEQ_NO

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
