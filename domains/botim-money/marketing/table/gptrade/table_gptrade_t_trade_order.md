---
id: tbl_gptrade_t_trade_order
object_type: Table
name: 修改时间 (t_trade_order)
aliases: [t_trade_order, gptrade.t_trade_order]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: gptrade schema DDL
tags: [marketing, gptrade]
sensitivity: normal
related_services: []
---

# 修改时间 (t_trade_order)

## 用途
物理表 `gptrade.t_trade_order`,主键 `trade_voucher_no`。修改时间。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trade_voucher_no` | bigint | 交易凭证号：18位，固定14+10位时间戳+4位序列+2位随机 |
| `trade_request_no` | bigint | 交易请求号 |
| `client_id` | varchar(32) | 客户端id |
| `payer_account_identity` | varchar(20) | 付款方账户标志 · 可空 |
| `payer_account_type` | varchar(10) | 付款方账户类型 · 可空 |
| `deduct_type` | varchar(10) | 扣款类型：C=收银台扣款，A=授权扣款 |
| `amount` | decimal(19, 4) | 交易金额 |
| `biz_product_code` | varchar(10) | 业务产品码 |
| `partner_id` | varchar(20) | 合作方ID |
| `is_auto_settle` | char | 是否自动结算：Y=是，N=否 |
| `trade_status` | varchar(10) | 交易状态：W=等待付款，PS=付款成功，C=关闭，TA=交易完成，CS=撤销成功，P=处理中，PF=付款失败 |
| `close_time` | timestamp | 关闭时间 · 可空 |
| `paid_time` | timestamp | 付款成功时间 · 可空 |
| `payment_voucher_no` | bigint | 支付订单 · 可空 |
| `finish_time` | timestamp | 结束时间 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(64) | 备注 · 可空 |
| `create_time` | timestamp(3) | 创建时间 |
| `update_time` | timestamp(3) | 待补 |

## 主键 / 索引
- 主键:`trade_voucher_no`
- `idx_close_time`:close_time
- `idx_trade_request_no`:trade_request_no
- `idx_update_time_client_id`:update_time, client_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
