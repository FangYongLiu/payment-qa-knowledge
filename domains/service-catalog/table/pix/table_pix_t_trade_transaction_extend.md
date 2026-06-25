---
id: tbl_pix_t_trade_transaction_extend
object_type: Table
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:a58de775-dd0b-457d-8a31-2bfc72c081d2
tags:
- pix
- transaction
- extend
subdomain: pix
module: null
sensitivity: normal
name: PIX交易扩展表 t_trade_transaction_extend
aliases:
- t_trade_transaction_extend
related_services:
- svc_pix
---

## 用途
PIX 交易扩展表 `pix.t_trade_transaction_extend`，用于存储 PIX 交易的扩展信息，包括交易 ID、交易时间、设备、商户等附加字段。与主交易表 [[tbl_pix_t_trade_transaction]] 通过 `trx_voucher_no` 关联。

## 关键列
| 列名 | 类型 | 说明 |
|---|---|---|
| trx_voucher_no | bigint | 交易凭证号(主键，关联主交易表) |
| trx_id | varchar(32) | 交易 ID |
| trx_time | timestamp | 交易时间 |
| device_id | varchar(100) | 设备 ID |
| merchant_id | varchar(50) | 商户 ID |
| merchant_name | varchar(...) | 商户名称(原文截断) |

## 主键/索引
- 主键(PK)：`trx_voucher_no`

## 校验点(QA 关注)
- `trx_voucher_no` 必须与 [[tbl_pix_t_trade_transaction]] 主表中存在的记录一一对应。
- `trx_id`、`trx_time`、`device_id`、`merchant_id`、`merchant_name` 等扩展字段在交易落库时是否完整写入。
- 字段长度限制：`trx_id` ≤32、`device_id` ≤100、`merchant_id` ≤50，超长截断或入库失败需关注。
- `trx_time` 与主表 `finish_time` 的时间一致性。
