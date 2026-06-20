---
id: tbl_pix_trade_transaction_extend
object_type: Table
domain: acquire-transaction
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:4538bf84-a043-4d3d-a9fd-d0fcbb9bc671
tags:
- pix
- schema
- extend
subdomain: null
module: null
sensitivity: normal
name: PIX交易扩展表 t_trade_transaction_extend
aliases:
- t_trade_transaction_extend
- pix.t_trade_transaction_extend
related_services: []
related_tables:
- tbl_pix_trade_transaction
- tbl_pix_refund_transaction
- tbl_pix_trade_relate_order
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
PIX schema 下的交易扩展信息表，用于存放 `pix.t_trade_transaction` 主交易记录之外的扩展字段。与 [[tbl_pix_trade_transaction]]、[[tbl_pix_refund_transaction]]、[[tbl_pix_trade_relate_order]] 同属 pix schema 的交易相关表族。

## 关键列
原文 ER 图中该表仅列出表名 `pix.t_trade_transaction_extend [Trade Transaction Extend]`，未给出具体字段定义。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 确认该扩展表与 [[tbl_pix_trade_transaction]] 的关联键(预期通过 `trx_voucher_no` 关联，原文未明示)。
- 字段定义在原文中缺失，需补充文档后再制定校验项。
