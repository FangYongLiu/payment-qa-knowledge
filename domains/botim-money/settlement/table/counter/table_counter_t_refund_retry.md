---
id: tbl_counter_t_refund_retry
object_type: Table
name: Refund Retry Record (t_refund_retry)
aliases: [t_refund_retry, counter.t_refund_retry]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# Refund Retry Record (t_refund_retry)

## 用途
物理表 `counter.t_refund_retry`,主键 `retry_id`。Refund Retry Record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `retry_id` | int | Retry Id · 可空 |
| `inst_order_no` | varchar(64) | Inst Order No |
| `fund_channel_code` | varchar(64) | Fund Channel Code · 可空 |
| `payment_order_no` | varchar(64) | Payment Order No · 可空 |
| `agl_code` | varchar(16) | AGL Code: CL/R2M/R2W |
| `amount` | decimal(19, 4) | Refund Amount |
| `currency` | char(3) | Currency |
| `accounting_id` | bigint | Accounting Id (tb_accounting) · 可空 |
| `biz_no` | varchar(64) | Biz No (t_voucher) · 可空 |
| `status` | varchar(4) | Status: I-Init, W-Wait Accounting, S-Success, F-Fail |
| `operator` | varchar(64) | Operator · 可空 |
| `memo` | varchar(512) | Memo · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`retry_id`
- `uk_inst_order_no`:inst_order_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
