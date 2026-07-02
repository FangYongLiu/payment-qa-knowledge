---
id: tbl_npss_t_relate_order
object_type: Table
name: unique  key for  idsct (t_relate_order)
aliases: [t_relate_order, npss.t_relate_order]
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

# unique  key for  idsct (t_relate_order)

## 用途
物理表 `npss.t_relate_order`,主键 `trx_voucher_no`。unique  key for  idsct。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trx_voucher_no` | bigint | Relate order |
| `related_order_id` | bigint | related order id |
| `order_type` | char(2) | order type: cr-credit refund |
| `member_id` | varchar(20) | member id |
| `amount` | decimal(19, 4) | amount |
| `currency` | char(3) | currency |
| `status` | char | status, I-init,S-success,F-failed |
| `id_sct` | varchar(32) | bank  order no · 可空 |
| `dbtr_bic` | varchar(11) | debit bic · 可空 |
| `cdtr_bic` | varchar(11) | credit bic · 可空 |
| `response_code` | varchar(10) | response  code · 可空 |
| `extension` | varchar(512) | extension · 可空 |
| `memo` | varchar(255) | memo · 可空 |
| `gmt_create` | timestamp | create type |
| `gmt_modified` | timestamp | modify time · 可空 |
| `gmt_finished` | timestamp | finish time · 可空 |
| `communicate_status` | varchar(2) | send-lock status: I/SI/SS/SF (dispatch lifecycle) · 可空 |

## 主键 / 索引
- 主键:`trx_voucher_no`
- `idx_tro_member_modified`:member_id, gmt_modified

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
