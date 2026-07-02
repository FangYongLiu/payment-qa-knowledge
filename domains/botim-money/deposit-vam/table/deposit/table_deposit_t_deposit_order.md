---
id: tbl_deposit_t_deposit_order
object_type: Table
name: 充值交易订单 (t_deposit_order)
aliases: [t_deposit_order, deposit.t_deposit_order]
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

# 充值交易订单 (t_deposit_order)

## 用途
物理表 `deposit.t_deposit_order`,主键 `TRADE_VOUCHER_NO`。充值交易订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `TRADE_VOUCHER_NO` | varchar(32) | 交易凭证号，主键，统一凭证 |
| `BIZ_PRODUCT_CODE` | varchar(16) | 产品编码 · 可空 |
| `AMOUNT` | decimal(15, 2) | 交易金额 · 可空 |
| `ACCESS_CHANNEL` | varchar(16) | 终端类型 · 可空 |
| `deposit_type` | varchar(8) | 交易类型: T=收银台交易 · 可空 |
| `GMT_SUBMIT` | timestamp | 交易发起时间 · 可空 |
| `TRADE_STATUS` | varchar(16) | 交易状态 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |
| `DEPOSIT_SRC_VOUCHER_NO` | varchar(64) | 原始充值凭证号（商户订单号） · 可空 |
| `PARTNER_ID` | varchar(32) | 平台方客户ID · 可空 |
| `PARTNER_NAME` | varchar(128) | 平台方客户名称 · 可空 |
| `ERROR_CODE` | varchar(16) | 错误编码 · 可空 |
| `ERROR_MESSAGE` | varchar(256) | 错误描述 · 可空 |
| `unity_result_code` | varchar(50) | 统一返回结果代码 · 可空 |
| `MEMBER_ID` | varchar(32) | 客户ID · 可空 |
| `ACCOUNT_NO` | varchar(32) | 用户账户 · 可空 |
| `ACCOUNT_TYPE` | varchar(16) | 账户类型 · 可空 |
| `REMARK` | varchar(128) | 备注 · 可空 |
| `EXT` | varchar(4000) | 扩展信息 · 可空 |
| `GMT_PAY_EXPIRED` | timestamp | 支付过期时间 · 可空 |
| `GMT_CLOSED` | timestamp | 交易关闭时间 · 可空 |
| `IDENTITY_ID` | varchar(64) | 标志ID · 可空 |
| `IDENTITY_TYPE` | varchar(16) | 标志类型 · 可空 |
| `SUB_STATUS` | varchar(16) | 交易子状态 · 可空 |
| `currency` | char(3) | 货币 中国CNY 阿联酋 AED 对应java类 Currency · 可空 |

## 主键 / 索引
- 主键:`TRADE_VOUCHER_NO`
- `IDX_DEPOSIT_ORDER_GMT_CRT`:GMT_CREATE
- `IDX_DEPOSIT_ORDER_GMT_EXP`:GMT_PAY_EXPIRED
- `IDX_DEPOSIT_ORDER_SRC_V_NO`:DEPOSIT_SRC_VOUCHER_NO
- `T_DEPOSIT_ORDER_GMT_MOD`:GMT_MODIFIED

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
