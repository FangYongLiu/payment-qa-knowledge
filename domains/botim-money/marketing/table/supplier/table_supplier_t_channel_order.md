---
id: tbl_supplier_t_channel_order
object_type: Table
name: 手机充值订单表 (t_channel_order)
aliases: [t_channel_order, supplier.t_channel_order]
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

# 手机充值订单表 (t_channel_order)

## 用途
物理表 `supplier.t_channel_order`,主键 `CHANNEL_ORDER_ID`。手机充值订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CHANNEL_ORDER_ID` | bigint(32) | 待补 |
| `SUPPLIER_ORDER_NO` | bigint(32) | 供应商平台订单号 |
| `CHANNEL_ORDER_NO` | varchar(32) | 渠道订单号 · 可空 |
| `order_amount` | decimal(15, 4) | 订单金额(结算货币单位：AED) · 可空 |
| `COMMISSION_AMOUNT` | decimal(15, 2) | 所得佣金 · 可空 |
| `PRODUCT_CODE` | varchar(32) | 产品编号 · 可空 |
| `PROVIDER_CODE` | varchar(32) | 供应商编号 · 可空 |
| `CHANNEL_CODE` | varchar(32) | 实际使用的渠道 · 可空 |
| `TARGET_ACCOUNT_NO` | varchar(256) | 目标账户编号 |
| `CURRENCY` | varchar(3) | 币种 |
| `STATUS` | char | 状态：A（待处理），C（已撤销），I（处理中），S（成功），F（失败） |
| `CHANNEL_RESP_CODE` | varchar(64) | 渠道响应码 · 可空 |
| `CHANNEL_RESP_MSG` | varchar(512) | 渠道响应描述 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |
| `tax_rate` | decimal(15, 4) | 交易发生时的费率 · 可空 |
| `order_receive_amount` | decimal(15, 4) | 用户会收到的话费金额(单位：国际) · 可空 |

## 主键 / 索引
- 主键:`CHANNEL_ORDER_ID`
- `idx_GMT_CREATE`:GMT_CREATE
- `idx_SUPPLIER_ORDER_NO`:SUPPLIER_ORDER_NO

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
