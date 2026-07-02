---
id: tbl_marketorder_t_phone_bill_order_detail
object_type: Table
name: 话费充值订单明细 (t_phone_bill_order_detail)
aliases: [t_phone_bill_order_detail, marketorder.t_phone_bill_order_detail]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketorder schema DDL
tags: [marketing, marketorder]
sensitivity: normal
related_services: []
---

# 话费充值订单明细 (t_phone_bill_order_detail)

## 用途
物理表 `marketorder.t_phone_bill_order_detail`,主键 `id`。话费充值订单明细。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `order_no` | bigint(18) | 订单编号 |
| `supplier_order_no` | varchar(32) | 供应商订单号 · 可空 |
| `channel_order_no` | varchar(32) | 渠道订单号 · 可空 |
| `phone` | varchar(16) | 电话号码 · 可空 |
| `face_value` | decimal(15, 4) | 面值 · 可空 |
| `goods_value` | decimal(15, 4) | 商品价值 · 可空 |
| `service_provider` | varchar(20) | 服务商:Du,Etisalat,Virgin,Swyp · 可空 |
| `package_type` | varchar(20) | 套餐类型: prePaid,postPaid · 可空 |
| `supplier_id` | varchar(64) | 供应商id · 可空 |
| `supplier_acc_no` | varchar(64) | 供应商账号 · 可空 |
| `channel_code` | varchar(32) | 渠道code · 可空 |
| `supplier_acc_type` | varchar(12) | 供应商账户类型 · 可空 |
| `channel_fee` | decimal(15, 4) | 渠道费用 · 可空 |
| `to_pay_profit` | decimal(15, 4) | 利润金额 · 可空 |
| `currency` | varchar(10) | 币种 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_order_no`:order_no (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
