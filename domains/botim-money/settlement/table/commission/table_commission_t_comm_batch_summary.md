---
id: tbl_commission_t_comm_batch_summary
object_type: Table
name: Commission Batch Summary (t_comm_batch_summary)
aliases: [t_comm_batch_summary, commission.t_comm_batch_summary]
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

# Commission Batch Summary (t_comm_batch_summary)

## 用途
物理表 `commission.t_comm_batch_summary`,主键 `summary_id`。Commission Batch Summary。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `summary_id` | bigint | Summary id: 8 date + 9 sequence |
| `batch_id` | bigint | Batch id: 8 date + 9 sequence |
| `partner_id` | varchar(20) | Partner ID · 可空 |
| `payee_id` | varchar(20) | Payee id |
| `member_id` | varchar(20) | Member id |
| `charger_account_no` | varchar(32) | Charger account no |
| `currency` | char(3) | Currency |
| `commission_amount` | decimal(19, 4) | Commission amount: Positive to credit, Negative to debit |
| `summary_status` | varchar(10) | Summary status: SP=Summary Process, AG=Accounting Ignored, AP=Accounting Process, AS=Accounting Success, AR=Accounting Retry |
| `detail_count` | bigint | Detail count |
| `payment_voucher_no` | bigint | Payment voucher no · 可空 |
| `retry_time` | timestamp | Retry time · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`summary_id`
- `idx_create_time_member_id`:create_time, member_id
- `uk_biz_key`:batch_id, member_id, currency, charger_account_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
