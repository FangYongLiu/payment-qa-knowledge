---
id: tbl_tobcredit_t_cb_instalment
object_type: Table
name: 还款计划表 (t_cb_instalment)
aliases: [t_cb_instalment, tobcredit.t_cb_instalment]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: tobcredit schema DDL
tags: [lending, tobcredit]
sensitivity: normal
related_services: []
---

# 还款计划表 (t_cb_instalment)

## 用途
物理表 `tobcredit.t_cb_instalment`,主键 `id`。还款计划表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `status` | smallint(5) | 状态： 0 待还款 1 完结 |
| `periods` | smallint(2) | 期数 |
| `check_time` | timestamp | 出帐日期 · 可空 |
| `due_time` | timestamp | 应还款日 |
| `check_amount` | decimal(19, 4) | 出帐金额 |
| `finish_repay_time` | timestamp | 完结时间 · 可空 |
| `partner_id` | varchar(32) | 商户 |
| `cope_capital` | decimal(19, 4) | 应还本金 |
| `cope_fee` | decimal(19, 4) | 应还利息 |
| `cope_penalty` | decimal(19, 4) | 应还罚息 |
| `already_repay_capital` | decimal(19, 4) | 已还本金 |
| `already_repay_fee` | decimal(19, 4) | 已还利息 |
| `already_repay_penalty` | varchar(19) | 已还罚息 |
| `reverse_way` | varchar(32) | 冲帐方式 · 可空 |
| `bill_no` | varchar(32) | 帐单号 |
| `memo` | varchar(512) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_partner_id`:partner_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
