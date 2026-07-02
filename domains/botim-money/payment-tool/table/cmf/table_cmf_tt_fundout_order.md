---
id: tbl_cmf_tt_fundout_order
object_type: Table
name: 出款订单 (tt_fundout_order)
aliases: [tt_fundout_order, cmf.tt_fundout_order]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# 出款订单 (tt_fundout_order)

## 用途
物理表 `cmf.tt_fundout_order`,主键 `INST_ORDER_ID`。出款订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `INST_ORDER_ID` | decimal(19) | 机构订单ID |
| `BANK_CODE` | varchar(32) | 开户行ID · 可空 |
| `BANK_NAME` | varchar(64) | 开户行名称 · 可空 |
| `BANK_BRANCH` | varchar(255) | 支行名称 · 可空 |
| `BANK_BRANCH_CODE` | varchar(32) | 联行号 · 可空 |
| `BANK_PROVINCE` | varchar(64) | 银行所属省份 · 可空 |
| `BANK_CITY` | varchar(64) | 银行所属城市 · 可空 |
| `AREA_CODE` | varchar(16) | 区域代码 · 可空 |
| `ACCOUNT_TYPE` | char | 账户类型：B（公司账户），C（个人账户） · 可空 |
| `ACCOUNT_NAME` | varchar(256) | 开户人姓名 · 可空 |
| `CARD_NO` | varchar(32) | 待补 · 可空 |
| `ACCOUNT_NO` | varchar(32) | 出款账号，储值帐号 · 可空 |
| `IBAN_NO` | varchar(32) | IBAN · 可空 |
| `SWIFT_CODE` | varchar(16) | 出款交换码 · 可空 |
| `BENEFICIARY_ADDRESS` | varchar(128) | 受益人地址 · 可空 |
| `INTERMEDIARY_BANK` | varchar(64) | 中间行 · 可空 |
| `CARD_TYPE` | varchar(8) | 卡类型：CC:贷记卡,DC:借记卡,SCC:准借记卡,PB:存折 · 可空 |
| `AGREEMENT_NO` | varchar(64) | 协议号,用于卡通提现 · 可空 |
| `PURPOSE` | varchar(128) | 用途 · 可空 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `GMT_CREATE` | timestamp | 创建时间 · 可空 |
| `PT_ID` | varchar(32) | 微汇通行证 · 可空 |

## 主键 / 索引
- 主键:`INST_ORDER_ID`
- `IDX_TT_FUNDOUT_ORDER_ACCTNAME`:ACCOUNT_NAME, ACCOUNT_NO
- `IDX_TT_FUNDOUT_ORDER_GMT`:GMT_CREATE

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
