---
id: tbl_cashierii_t_order_log
object_type: Table
name: Order Log (t_order_log)
aliases: [t_order_log, cashierii.t_order_log]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cashierii schema DDL
tags: [payment-core, cashierii]
sensitivity: normal
related_services: []
---

# Order Log (t_order_log)

## 用途
物理表 `cashierii.t_order_log`,主键 `log_id`。Order Log。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `log_id` | bigint | Log ID, 前八后九 |
| `event_code` | varchar(32) | Event Code |
| `member_id` | varchar(20) | Member ID |
| `voucher_no` | bigint | Voucher No · 可空 |
| `order_token` | varchar(70) | Order Token · 可空 |
| `ip` | varchar(16) | IP · 可空 |
| `log_time` | timestamp(3) | Log Time |
| `code` | varchar(8) | Code · 可空 |
| `message` | varchar(255) | Message · 可空 |
| `tid` | varchar(100) | TID · 可空 |
| `extension` | varchar(255) | Extension · 可空 |

## 主键 / 索引
- 主键:`log_id`
- `idx_log_time`:log_time
- `idx_order_token`:order_token
- `idx_voucher_no`:voucher_no

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
