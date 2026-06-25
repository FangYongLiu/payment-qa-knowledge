---
id: tbl_pix_t_trade_transaction
object_type: Table
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:a58de775-dd0b-457d-8a31-2bfc72c081d2
tags:
- PIX
- 交易主表
subdomain: pix
module: null
sensitivity: normal
name: PIX交易表 t_trade_transaction
aliases:
- pix.t_trade_transaction
related_services:
- svc_pix
---

## 用途
PIX 渠道交易主表(schema: `pix`，表名 `t_trade_transaction`)，记录 PIX 渠道每笔交易的凭证号、会员、金额、币种、汇率/保证金版本、利润、交易状态及结果码等核心信息。退款交易表 `t_refund_transaction` 通过 `orig_trx_voucher_no` 反查本表；扩展信息记录在 `t_trade_transaction_extend`。

## 关键列
- `trx_voucher_no` bigint：交易凭证号(主键)
- `channel_code` varchar(32)：渠道编码
- `order_type` varchar(32)：订单类型
- `member_id` varchar(20)：会员 ID
- `transaction_amount` decimal(19,4) / `transaction_currency` char(3)：交易金额与币种
- `pay_amount` decimal(19,4) / `pay_currency` char(3)：支付金额与币种
- `rate_version` bigint：汇率版本
- `margin_version` bigint：保证金版本
- `profit_amount` decimal(19,4)：利润金额
- `transaction_status` varchar(10)：交易状态
- `unity_result_code` varchar(50)：统一结果码
- `channel_result_code` varchar(50)：渠道结果码
- `finish_time` timestamp(3)：完成时间

## 主键/索引
- 主键：`trx_voucher_no`
- 关联：被 [[tbl_pix_t_refund_transaction]] 通过 `orig_trx_voucher_no` 引用；与 [[tbl_pix_t_trade_transaction_extend]] 通过 `trx_voucher_no` 1:1 关联。

## 校验点(QA 关注)
- `trx_voucher_no` 唯一性，且与扩展表/退款表的引用一致。
- `transaction_amount`/`pay_amount` 为 decimal(19,4)，币种为 char(3)，注意精度与币种合法性。
- `rate_version`、`margin_version` 应能回溯到对应版本快照，影响 `pay_amount` 与 `profit_amount` 计算。
- `transaction_status` 取值受限于 varchar(10)，需与状态机定义一致。
- `unity_result_code` 与 `channel_result_code` 的映射关系：终态时是否同步落库，便于排查渠道差异。
- `finish_time` 仅在终态写入，未终态记录应为空或保持业务约定。
- `channel_code`/`order_type`/`member_id` 非空与有效性校验。
