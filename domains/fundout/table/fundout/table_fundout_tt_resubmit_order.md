---
id: tbl_fundout_tt_resubmit_order
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
- tt_resubmit_order
subdomain: fundout
module: null
sensitivity: normal
name: 出款重提交(tt_resubmit_order)
aliases:
- tt_resubmit_order
related_services:
- svc_fundout
related_scenarios: []
---
# 出款重提交(tt_resubmit_order)

## 用途
出款重提交。属 fundout 库,由 [[svc_fundout]] 读写。

## 关联关系
- **所属服务**:[[svc_fundout]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `VOUCHER_NO` | varchar(32) | PK / NOT NULL | 统一凭证号，外部传入 |
| `VOUCHER_TYPE` | varchar(32) |  | 凭证类型 |
| `STATUS` | varchar(16) |  | 重处理状态 |
| `HANDLER` | varchar(16) |  | 处理订单服务器 |
| `RESULT` | varchar(2000) |  | 处理结果 |
| `GMT_CREATE` | timestamp |  |  |
| `GMT_MODIFY` | timestamp |  |  |

## 主键 / 索引
- 主键:(`VOUCHER_NO`)
- 索引:
  - `I_HANDLER_STATUS` (HANDLER, STATUS)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
