---
id: tbl_commission_t_comm_detail
object_type: Table
name: Commission Detail (t_comm_detail)
aliases: [t_comm_detail, commission.t_comm_detail]
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

# Commission Detail (t_comm_detail)

## 用途
物理表 `commission.t_comm_detail`,主键 `detail_id`。Commission Detail。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `detail_id` | bigint | Detail id: 8 date + 9 sequence |
| `detail_voucher_no` | bigint | Detail voucher no |
| `detail_type` | varchar(10) | Detail type: TT=Tradeii trade, TR=Tradeii refund |
| `orig_detail_voucher_no` | bigint | Original detail voucher no · 可空 |
| `effect_amount` | decimal(19, 4) | Effect amount |
| `currency` | char(3) | Currency |
| `comm_config_id` | bigint | Commission Config id |
| `partner_id` | varchar(20) | Partner id |
| `biz_product_code` | varchar(10) | Biz product code |
| `payee_id` | varchar(20) | Payee id |
| `member_id` | varchar(20) | Member id |
| `charger_account_no` | varchar(32) | Charge account no |
| `commission_amount` | decimal(19, 4) | Commission amount: Positive to credit, Negative to debit |
| `match_config_time` | timestamp | Match config time · 可空 |
| `match_sync_time` | timestamp | Match sync time |
| `detail_status` | char | Detail status: I=Init, B=Batched |
| `batch_id` | bigint | Batch id · 可空 |
| `commission_type` | varchar(10) | C/R · 可空 |
| `config_version_id` | bigint | Comm Config Version Id · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`detail_id`
- `uk_biz_key`:detail_voucher_no, member_id (UNIQUE)
- `idx_batch_mark`:match_sync_time, partner_id, biz_product_code, detail_status
- `idx_batch_no`:batch_id
- `idx_orig_detail_voucher_no`:orig_detail_voucher_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
