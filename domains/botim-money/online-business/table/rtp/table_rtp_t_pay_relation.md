---
id: tbl_rtp_t_pay_relation
object_type: Table
name: Pay Relation (t_pay_relation)
aliases: [t_pay_relation, rtp.t_pay_relation]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rtp schema DDL
tags: [online-business, rtp]
sensitivity: normal
related_services: []
---

# Pay Relation (t_pay_relation)

## 用途
物理表 `rtp.t_pay_relation`,主键 `relation_id`。Pay Relation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `relation_id` | bigint | Relation ID: 8 digits date time + 9 digits sequence |
| `pay_trade_no` | bigint | Pay Trade No |
| `payer_order_no` | bigint | Payer Order No |
| `pay_relation_status` | varchar(10) | Pay Relation Status: P=Process, F=Fail, S=Success, CP=CancelProcess, CS=CancelSuccess |
| `cancel_voucher_no` | bigint | Cancel Voucher No · 可空 |

## 主键 / 索引
- 主键:`relation_id`
- `idx_pay_trade_no`:pay_trade_no
- `idx_payer_order_no`:payer_order_no

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
