---
id: tbl_deposit_t_payment_party
object_type: Table
name: 支付参与方表 (t_payment_party)
aliases: [t_payment_party, deposit.t_payment_party]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: deposit schema DDL
tags: [deposit-vam, deposit]
sensitivity: normal
related_services: []
---

# 支付参与方表 (t_payment_party)

## 用途
物理表 `deposit.t_payment_party`,主键 `ID`。支付参与方表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | varchar(11) | 参与方ID，主键，SEQ_PAYMENT_PARTY |
| `PAYMENT_VOUCHER_NO` | varchar(32) | 支付凭证号 · 可空 |
| `MEMBER_ID` | varchar(32) | 客户ID |
| `PARTY_ROLE` | varchar(16) | 角色 · 可空 |
| `ACCOUNT` | varchar(32) | 账户 · 可空 |
| `EXT` | varchar(4000) | 扩展参数 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
