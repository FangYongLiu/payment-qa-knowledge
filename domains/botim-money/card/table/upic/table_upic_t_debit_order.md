---
id: tbl_upic_t_debit_order
object_type: Table
name: 借记订单 (t_debit_order)
aliases: [t_debit_order, upic.t_debit_order]
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

# 借记订单 (t_debit_order)

## 用途
物理表 `upic.t_debit_order`,主键 `trx_voucher_no`。借记订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trx_voucher_no` | bigint | 借记凭证 凭证服务产生 |
| `message_id` | varchar(50) | 记账消息id |
| `debit_order_type` | varchar(10) | 借记订单类型：MPC=商户码, CPC=用户码, HCE=NFC |
| `product_order_no` | bigint | 产品订单号 · 可空 |
| `member_id` | varchar(20) | 会员id |
| `bill_amount` | decimal(19, 4) | 账单金额 |
| `bill_currency` | char(3) | 账单币种 |
| `debit_order_status` | varchar(10) | 借记订单状态：P=处理中，S=成功，F=失败 |
| `pay_channel` | varchar(10) | 支付方式 · 可空 |
| `unity_result_code` | varchar(64) | 统一返回码 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |
| `finish_time` | timestamp | 结束时间 · 可空 |

## 主键 / 索引
- 主键:`trx_voucher_no`
- `idx_message_id`:message_id
- `idx_product_order_no`:product_order_no
- `idx_update_time_member_id`:update_time, member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
