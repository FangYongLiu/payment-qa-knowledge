---
id: tbl_pix_t_trade_transaction_extend
object_type: Table
domain: acquire-transaction
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:49c5a737-48df-4836-9baa-414f1de4f810
tags:
- pix
- extend
subdomain: null
module: null
sensitivity: normal
name: pix交易扩展表 t_trade_transaction_extend
aliases:
- t_trade_transaction_extend
related_services: []
related_tables:
- tbl_pix_t_trade_transaction
- tbl_pix_t_refund_transaction
- tbl_pix_t_trade_relate_order
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
pix schema 下交易事务的扩展信息表 `t_trade_transaction_extend`，用于承载主交易表 `t_trade_transaction` 之外的扩展字段。原文 ER 图中仅列出表名 `[Trade Transaction Extend]`，未给出字段定义。

## 关键列
原文未提供字段清单。

## 主键/索引
原文未提供主键与索引信息。

## 校验点(QA 关注)
- 与 [[tbl_pix_t_trade_transaction]] 的关联关系需结合实际 schema 确认(原文 ER 图未展开本表字段)。
- 字段、主键、索引信息需以数据库实际 DDL 为准，本文档不做推断。
