---
id: tbl_payment_tb_party_account
object_type: Table
name: 清结算参与方帐户，供特殊指定帐户使用 (tb_party_account)
aliases: [tb_party_account, payment.tb_party_account]
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

# 清结算参与方帐户，供特殊指定帐户使用 (tb_party_account)

## 用途
物理表 `payment.tb_party_account`,主键 `ID`。清结算参与方帐户，供特殊指定帐户使用。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint | 帐户ID · 可空 |
| `AGREEMENT_ID` | decimal(11) | 协议ID，主键:SEQ_CLEARING_AGREEMENT |
| `CLEARING_CODE` | varchar(32) | 清算代码 · 可空 |
| `PARTY_ROLE` | varchar(10) | 参与角色 |
| `PARTY_ID` | varchar(64) | 参与方ID · 可空 |
| `ACCOUNT_NO` | varchar(32) | 结算帐号 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
