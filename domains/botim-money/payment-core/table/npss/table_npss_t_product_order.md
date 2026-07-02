---
id: tbl_npss_t_product_order
object_type: Table
name: Unique Trx Voucher No Key (t_product_order)
aliases: [t_product_order, npss.t_product_order]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# Unique Trx Voucher No Key (t_product_order)

## 用途
物理表 `npss.t_product_order`,主键 `product_order_no`。Unique Trx Voucher No Key。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `product_order_no` | bigint | 产品订单号：交易请求号 |
| `order_type` | char(3) | 订单类型：SM=Send Money, R2P=Request to Pay ,SB=Split Bill |
| `sub_order_type` | varchar(10) | 订单子类型 · 可空 |
| `device_id` | varchar(64) | 设备id |
| `member_id` | varchar(20) | 会员id |
| `token` | varchar(32) | token |
| `merchant_name` | varchar(128) | 商户名称 |
| `transaction_amount` | decimal(19, 4) | 交易金额 |
| `transaction_currency` | char(3) | 交易币种 |
| `transfer_amount` | decimal(19, 4) | 转账金额 |
| `fee_amount` | decimal(19, 4) | 手续费金额 |
| `transfer_type` | char(3) | 转账类型,I2I-内转内,I2O-内转外,O2I-外转内 · 可空 |
| `trans_source` | char(2) | AT-aani transfer,SM-send money · 可空 |
| `account_name` | varchar(128) | 接收方用户名 · 可空 |
| `account_type` | varchar(10) | 接收方账户类型: email=邮箱，mobile=手机，eid=证件 · 可空 |
| `account_value` | varchar(32) | 接收方账户值 · 可空 |
| `id_sct` | varchar(32) | 银行订单号 · 可空 |
| `memo` | varchar(140) | memo · 可空 |
| `message_id` | varchar(50) | 消息id · 可空 |
| `status` | char(2) | 产品订单状态：P=已准备，F=已失败，VS=验证通过，C=已关闭或付款失败，S=付款成功 |
| `unity_result_code` | varchar(64) | 统一返回码 · 可空 |
| `trx_voucher_no` | bigint | 借记交易凭证 · 可空 |
| `extension` | varchar(512) | Extension · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `gmt_finished` | timestamp | 结束时间 · 可空 |
| `gmt_expire` | timestamp | 过期时间 · 可空 |

## 主键 / 索引
- 主键:`product_order_no`
- `idx_update_time_member_id`:gmt_modified, member_id
- `uk_product_id_sct`:id_sct

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
