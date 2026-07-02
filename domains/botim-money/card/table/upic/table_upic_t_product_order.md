---
id: tbl_upic_t_product_order
object_type: Table
name: 产品订单 (t_product_order)
aliases: [t_product_order, upic.t_product_order]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: upic schema DDL
tags: [card, upic]
sensitivity: normal
related_services: []
---

# 产品订单 (t_product_order)

## 用途
物理表 `upic.t_product_order`,主键 `product_order_no`。产品订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `product_order_no` | bigint | 产品订单号：交易请求号 |
| `product_order_type` | varchar(10) | 产品订单类型：MPC=商户码，CPC=用户码 |
| `device_id` | varchar(64) | 设备id |
| `member_id` | varchar(20) | 会员id |
| `token` | varchar(32) | token |
| `merchant_name` | varchar(128) | 商户名称 |
| `transaction_currency` | char(3) | 交易币种 |
| `transaction_amount` | decimal(19, 4) | 交易金额 |
| `tip_fee_type` | varchar(10) | 小费类型：TIP=小费，FF=固定费用，FP=比例费用 · 可空 |
| `tip_fee_amount` | decimal(19, 4) | 小费金额 · 可空 |
| `bill_exchange_rate` | decimal(10, 4) | 扣款汇率 · 可空 |
| `estimated_bill_amount` | decimal(19, 4) | 预计扣款金额 |
| `message_id` | varchar(50) | 消息id · 可空 |
| `product_order_status` | varchar(10) | 产品订单状态：P=已准备，F=已失败，VS=验证通过，C=已关闭或付款失败，S=付款成功 |
| `unity_result_code` | varchar(64) | 统一返回码 · 可空 |
| `trx_voucher_no` | bigint | 借记交易凭证 · 可空 |
| `extension` | varchar(1000) | Extension · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |
| `finish_time` | timestamp | 结束时间 · 可空 |

## 主键 / 索引
- 主键:`product_order_no`
- `idx_update_time_member_id`:update_time, member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
