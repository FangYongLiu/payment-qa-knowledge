---
id: tbl_payment_tb_funds_channel_info
object_type: Table
name: 资金渠道信息 (tb_funds_channel_info)
aliases: [tb_funds_channel_info, payment.tb_funds_channel_info]
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

# 资金渠道信息 (tb_funds_channel_info)

## 用途
物理表 `payment.tb_funds_channel_info`,主键 `CHANNEL_INFO_ID`。资金渠道信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CHANNEL_INFO_ID` | int | 待补 · 可空 |
| `FUNDS_CHANNEL` | varchar(32) | 资金渠道 |
| `IS_REFUND` | char | 是否退款 |
| `WAIT_ACCOUNT` | varchar(32) | 待清算帐户 · 可空 |
| `BANK_ACCOUNT` | varchar(32) | 银存帐户 · 可空 |
| `FUND_PROP` | char(2) | 资金属性：CA-贷记资金 DA-借记资金 · 可空 |
| `SEND_GLIDE` | char | 是否发送入账流水 |
| `GMT_EFFECT` | timestamp | 生效时间 |
| `GMT_EXPIRED` | timestamp | 失效时间，空则代表永不失效 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`CHANNEL_INFO_ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
