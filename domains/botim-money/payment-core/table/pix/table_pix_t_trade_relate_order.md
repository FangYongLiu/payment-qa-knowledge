---
id: tbl_pix_t_trade_relate_order
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:49c5a737-48df-4836-9baa-414f1de4f810
tags:
- pix
- trade-relate
- association
subdomain: pix
module: SD-Transaction
sensitivity: normal
name: pix交易关联订单表 t_trade_relate_order
aliases:
- t_trade_relate_order
- pix.t_trade_relate_order
related_services:
- svc_pix
---

## 用途
pix schema 下的交易关联订单表，用于将交易请求 (`trade_request_no`) 与交易凭证号 (`trx_voucher_no`) 进行关联，承载交易/退款的请求-凭证映射，以及关联的交易类型、订单状态与统一结果码。可关联到 [[tbl_pix_t_trade_transaction]] 与 [[tbl_pix_t_refund_transaction]]，整体 ER 见 [[pix-sd-transaction-er-overview]]。

## 关键列
- `trade_request_no` bigint：交易请求号，主键。
- `transaction_type` varchar(10)：交易类型（区分交易/退款等）。
- `trx_voucher_no` bigint：关联的交易凭证号，对应主表/退款表 PK。
- `trade_type` varchar(10)：交易具体类型。
- `trade_order_status` varchar(10)：关联订单状态。
- `unity_result_code` varchar(50)：统一结果码。

## 主键/索引
- 主键 PK：`trade_request_no`。
- 原文未列出其他索引（如基于 `trx_voucher_no` 的查询索引未在 ER 中体现）。

## 校验点(QA 关注)
- `trade_request_no` 唯一性：作为 PK 不能重复，重放/重试场景需保证幂等。
- `trx_voucher_no` 关联一致性：必须能在 [[tbl_pix_t_trade_transaction]] 或 [[tbl_pix_t_refund_transaction]] 中找到对应记录；交易/退款类型应与 `transaction_type` 匹配。
- `transaction_type` 与 `trade_type` 取值需符合枚举约束（原文未列出枚举值，需结合代码侧校验）。
- `trade_order_status` 状态流转校验：与主交易表 `transaction_status` 的一致性。
- `unity_result_code` 与主表的 `unity_result_code` 在最终态下应一致。
- 字段长度：`transaction_type`/`trade_type`/`trade_order_status` 限 10 位，`unity_result_code` 限 50 位，超长需在写入前截断或拒绝。
