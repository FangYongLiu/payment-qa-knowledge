---
id: tbl_collection_t_col_bill
object_type: Table
name: t_col_bill (t_col_bill)
aliases: [t_col_bill, collection.t_col_bill]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# t_col_bill (t_col_bill)

## 用途
物理表 `collection.t_col_bill`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `update_by` | varchar(100) | 修改人 · 可空 |
| `bill_no` | varchar(64) | 账单号 |
| `member_id` | varchar(50) | 会员ID |
| `due_time` | timestamp | 还款时间 · 可空 |
| `current_user_uid` | varchar(64) | 当前催收员id · 可空 |
| `will_repay_capital` | decimal(19, 2) | 应还本金 · 可空 |
| `will_repay_fee` | decimal(19, 2) | 应还手续费 · 可空 |
| `will_repay_penalty` | decimal(19, 2) | Should repay penalty · 可空 |
| `already_repay_capital` | decimal(19, 2) | 已还本金 · 可空 |
| `already_repay_penalty` | decimal(19, 2) | 已还利息 · 可空 |
| `already_repay_fee` | decimal(19, 2) | 已还手续费 · 可空 |
| `is_repay` | tinyint | 是否有还款 0初始 1还款 |
| `status` | tinyint | 状态 -1退款 0:初始 1待分配 2再分配 3在催 4完结  |
| `last_follow_status` | tinyint | 联系结果 · 可空 |
| `last_contact_date` | timestamp | 联系时间 · 可空 |
| `promise_repayment_date` | timestamp | 承诺还款时间 · 可空 |
| `due_time_amount` | decimal(19, 2) | 逾期时逾期本金 · 可空 |
| `last_repay_time` | timestamp | 最后一次还款时间 · 可空 |
| `finish_due_days` | int(4) | 完结时逾期天数 · 可空 |
| `finish_time` | timestamp | 完结时间 · 可空 |
| `product` | tinyint | 产品 cashnow1 paylater2 |
| `times` | tinyint(5) | 借款次数 · 可空 |
| `ptp_count` | smallint(5) | ptp次数 · 可空 |
| `bp_count` | smallint(5) | bp次数 · 可空 |
| `is_extension` | tinyint(5) | 是否展期 · 可空 |
| `finish_type` | tinyint(5) | 完结类型 1普通 2展期  · 可空 |
| `priority` | tinyint(5) | 优先级 |
| `score` | decimal(11, 10) | 模型分数 |
| `oper_system` | tinyint(5) | 借款时操作系统 1:android 2:ios · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_current_user_uid`:current_user_uid
- `idx_due_time`:due_time
- `idx_member_id`:member_id
- `idx_promise_repayment_date`:promise_repayment_date
- `idx_status_cuid_due_time`:status, current_user_uid, due_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
