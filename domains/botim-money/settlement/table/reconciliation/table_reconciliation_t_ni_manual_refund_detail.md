---
id: tbl_reconciliation_t_ni_manual_refund_detail
object_type: Table
name: NI Manual Refund Detail (t_ni_manual_refund_detail)
aliases: [t_ni_manual_refund_detail, reconciliation.t_ni_manual_refund_detail]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# NI Manual Refund Detail (t_ni_manual_refund_detail)

## 用途
物理表 `reconciliation.t_ni_manual_refund_detail`,主键 `detail_id`。NI Manual Refund Detail。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `detail_id` | bigint | Detail Id: 8 digits date + 9 digits sequence |
| `batch_id` | bigint | Batch Id |
| `inst_order_no` | varchar(64) | Inst Order No |
| `merchant_id` | varchar(20) | Merchant Id · 可空 |
| `card_number` | varchar(32) | Card Number · 可空 |
| `auth_code` | varchar(32) | Auth Code · 可空 |
| `amount` | decimal(19, 4) | Amount |
| `currency` | char(3) | Currency |
| `status` | char | Status: I-Initial S-Success F-Failed |
| `result_message` | varchar(50) | result_message · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`detail_id`
- `idx_batchId`:batch_id
- `idx_instOrderNo`:inst_order_no
- `idx_merchantId_cardNo_authCode`:merchant_id, card_number, auth_code

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
