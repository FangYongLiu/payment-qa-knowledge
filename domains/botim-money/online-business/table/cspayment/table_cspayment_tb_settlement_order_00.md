---
id: tbl_cspayment_tb_settlement_order_00
object_type: Table
name: 结算指令 (tb_settlement_order_00)
aliases: [tb_settlement_order_00, cspayment.tb_settlement_order_00]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cspayment schema DDL
tags: [online-business, cspayment]
sensitivity: normal
related_services: []
---

# 结算指令 (tb_settlement_order_00)

## 用途
物理表 `cspayment.tb_settlement_order_00`,主键 `SETTLEMENT_ORDER_ID`。结算指令。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `SETTLEMENT_ORDER_ID` | varchar(32) | 主键，序列号SEQ_SETTLEMENT_ORDER |
| `CLEARING_SESSION_ID` | varchar(32) | 清算场次标识:SEQ_CLEARING_SESSION_ID |
| `PAYMENT_SEQ_NO` | varchar(32) | 支付流水号 · 可空 |
| `SUITE_NO` | decimal(18) | 指令套号:SEQ_SETTLEMENT_ORDER_SUITE |
| `PARTY_ROLE` | varchar(32) | 参与角色 |
| `PARTY_ID` | varchar(64) | 参与方ID · 可空 |
| `ACCOUNT_NO` | varchar(32) | 结算帐号 · 可空 |
| `DC_DIRECTION` | char | 借贷方向，D-借方；C-贷方 |
| `CURRENCY` | char(3) | 币种 |
| `AMOUNT` | decimal(15, 4) | 金额 |
| `FREEZE_TAG` | char | 冻结标记：F-冻结；N-正常 · 可空 |
| `RED_BLUE_TAG` | char | 红蓝标记 · 可空 |
| `FUND_PROP` | char(2) | 资金属性：CA-贷记资金 DA-借记资金 BI-借贷皆可 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `CLEARING_CODE` | varchar(32) | 清算编码 · 可空 |

## 主键 / 索引
- 主键:`SETTLEMENT_ORDER_ID`
- `IDX_SO_GMTMODIFIED_00`:GMT_MODIFIED
- `I_TB_SORDER_CSESSIONID_00`:CLEARING_SESSION_ID
- `I_TB_SORDER_PSEQNO_00`:PAYMENT_SEQ_NO

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
