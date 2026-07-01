---
id: tbl_fundout_tt_fund_prepare
object_type: Table
domain: fundout
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (fundout schema) 2026-06-25
tags:
- fundout
- fundout
- tt_fund_prepare
subdomain: fundout
module: null
sensitivity: normal
name: Fund Prepare(tt_fund_prepare)
aliases:
- tt_fund_prepare
related_services:
- svc_fundout
related_scenarios: []
---
# Fund Prepare(tt_fund_prepare)

## 用途
Fund Prepare。属 fundout 库,由 [[svc_fundout]] 读写。

## 关联关系
- **所属服务**:[[svc_fundout]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `fund_prepare_voucher_no` | bigint | PK / NOT NULL | Fund Prepare Voucher No |
| `orig_fund_prepare_voucher_no` | bigint |  | Orig Fund Prepare Voucher No |
| `fundout_order_no` | varchar(32) | NOT NULL | Fundout Order No |
| `fund_prepare_type` | varchar(10) | NOT NULL | Fund Prepare Type: T=Transfer, R=Rollback |
| `biz_product_code` | varchar(32) | NOT NULL | Biz Product Code |
| `payer_account` | varchar(32) | NOT NULL | Payer Account |
| `amount` | decimal(19,4) | NOT NULL | Amount |
| `currency` | char(3) | NOT NULL | Currency |
| `fund_prepare_status` | varchar(10) | NOT NULL | Fund Prepare Status: init, process, success, failed, refunded |
| `extension` | varchar(255) |  | Extension |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`fund_prepare_voucher_no`)
- 索引:
  - `idx_fundout_order_no` (fundout_order_no)
  - `idx_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
