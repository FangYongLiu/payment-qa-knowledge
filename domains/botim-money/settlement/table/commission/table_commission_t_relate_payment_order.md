---
id: tbl_commission_t_relate_payment_order
object_type: Table
name: Relate Payment Order (t_relate_payment_order)
aliases: [t_relate_payment_order, commission.t_relate_payment_order]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: commission schema DDL
tags: [settlement, commission]
sensitivity: normal
related_services: []
---

# Relate Payment Order (t_relate_payment_order)

## 用途
物理表 `commission.t_relate_payment_order`,主键 `payment_voucher_no`。Relate Payment Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `payment_voucher_no` | bigint | Payment voucher no: 8 date + 9 sequence |
| `order_type` | varchar(10) | Order type: SA=Summary Accounting |
| `order_voucher_no` | bigint | Order voucher no |
| `payment_status` | char | Payment status: P=Process, S=Success, F=Fail |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`payment_voucher_no`
- `idx_order_voucher_no`:order_voucher_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
