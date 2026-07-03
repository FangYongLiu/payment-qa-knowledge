---
id: tbl_socialpay_t_redpkg_receive
object_type: Table
name: 红包领取记录 (t_redpkg_receive)
aliases: [t_redpkg_receive, socialpay.t_redpkg_receive]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: socialpay schema DDL
tags: [online-business, socialpay]
sensitivity: normal
related_services: [svc_socialpay]
---

# 红包领取记录 (t_redpkg_receive)

## 用途
物理表 `socialpay.t_redpkg_receive`,主键 `RECEIVE_VOUCHER_NO`。红包领取记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `RECEIVE_VOUCHER_NO` | varchar(32) | 待补 |
| `RECEIVE_TRADE_NO` | varchar(32) | 待补 |
| `OUT_TRADE_NO` | varchar(32) | 待补 |
| `PAYEE_UID` | varchar(32) | 收款人UID |
| `PAYEE_MEMBER_ID` | varchar(32) | 收款会员ID · 可空 |
| `AMOUNT` | decimal(15, 4) | 领取金额 |
| `RECEIVE_TIME` | timestamp | 领取时间 |
| `IS_LUCKY` | char | 是否手气最佳：Y 是 · 可空 |
| `RECEIVE_STATUS` | varchar(15) | 领取状态 |
| `GMT_CREATED` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 更新时间 |
| `EXTENSION` | varchar(500) | 扩展参数，JSON字符串 · 可空 |
| `PAYER_UID` | varchar(32) | 付款人uid |

## 主键 / 索引
- 主键:`RECEIVE_VOUCHER_NO`
- `t_redpkg_receive_out_trade_no_index`:OUT_TRADE_NO
- `t_redpkg_receive_payee_uid_index`:PAYEE_UID

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
