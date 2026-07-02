---
id: tbl_supplier_t_supplier_order
object_type: Table
name: 供应商订单表 (t_supplier_order)
aliases: [t_supplier_order, supplier.t_supplier_order]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: supplier schema DDL
tags: [marketing, supplier]
sensitivity: normal
related_services: []
---

# 供应商订单表 (t_supplier_order)

## 用途
物理表 `supplier.t_supplier_order`,主键 `SUPPLIER_ORDER_ID`。供应商订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `SUPPLIER_ORDER_ID` | bigint(32) | 待补 |
| `LIFE_ORDER_NO` | varchar(32) | 生活平台订单号 |
| `CHANNEL_ORDER_NO` | varchar(32) | 渠道订单号 · 可空 |
| `COMMISSION_AMOUNT` | decimal(15, 2) | 所得佣金 · 可空 |
| `ACTUAL_COMMISSION_AMOUNT` | decimal(15, 4) | 实际佣金 · 可空 |
| `OFFER_CHANNELS` | varchar(1024) | 还可使用的渠道列表 · 可空 |
| `CURRENCY` | varchar(3) | 币种 |
| `PAYMENT_NOTIFY_STATUS` | varchar(1) | 支付结果通知状态：S（通知成功），F（通知失败），N（未通知） |
| `STATUS` | varchar(1) | 状态：A（待处理），C（已撤销），I（处理中），S（成功），F（失败） |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `EXTENSION` | varchar(2048) | 拓展信息 · 可空 |
| `target_account_no` | varchar(256) | 目标账户编号 |
| `order_amount` | decimal(15, 4) | 订单金额(结算货币单位：AED) · 可空 |
| `SUPPLIER_TYPE` | varchar(32) | 供应类型，Mobile_top_up：手机充值供应商 |
| `AVA_CHANNELS` | varchar(1024) | 还可使用的渠道列表 · 可空 |
| `member_id` | varchar(32) | 会员编号 · 可空 |
| `tax_rate` | decimal(15, 4) | 交易发生时的费率 · 可空 |
| `pay_amount` | decimal(15, 4) | 用户实际支付金额(单位：AED) · 可空 |
| `order_receive_amount` | decimal(15, 4) | 用户会收到的话费金额(单位：国际) |

## 主键 / 索引
- 主键:`SUPPLIER_ORDER_ID`
- `uk_lifeOrderNo`:LIFE_ORDER_NO (UNIQUE)
- `idx_GMT_CREATE`:GMT_CREATE
- `idx_mod_status`:GMT_MODIFIED, STATUS

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
