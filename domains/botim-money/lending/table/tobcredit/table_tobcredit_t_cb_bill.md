---
id: tbl_tobcredit_t_cb_bill
object_type: Table
name: 帐单表 (t_cb_bill)
aliases: [t_cb_bill, tobcredit.t_cb_bill]
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

# 帐单表 (t_cb_bill)

## 用途
物理表 `tobcredit.t_cb_bill`,主键 `id`。帐单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `amount` | decimal(19, 4) | 金额 |
| `partner_id` | varchar(20) | 商户 |
| `check_time` | timestamp | 出帐时间 |
| `bill_no` | varchar(64) | 帐单时间 |
| `progress` | smallint(5) | 状态: 1 待还款， 2 还款中， 3 完结， -3 还款失败 |
| `finish_repay_time` | timestamp | 完结时间 · 可空 |
| `bill_start_time` | timestamp | 帐单开始时间 |
| `bill_end_time` | timestamp | 帐单结束时间 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_partner_id`:partner_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
