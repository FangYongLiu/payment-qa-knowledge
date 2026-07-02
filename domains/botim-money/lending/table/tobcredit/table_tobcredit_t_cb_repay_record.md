---
id: tbl_tobcredit_t_cb_repay_record
object_type: Table
name: 还款记录 (t_cb_repay_record)
aliases: [t_cb_repay_record, tobcredit.t_cb_repay_record]
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

# 还款记录 (t_cb_repay_record)

## 用途
物理表 `tobcredit.t_cb_repay_record`,主键 `id`。还款记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `bill_no` | varchar(64) | 帐单号 · 可空 |
| `repay_amount` | decimal(19, 4) | 还款金额 · 可空 |
| `repay_way` | varchar(128) | 还款方式 · 可空 |
| `status` | smallint(5) | 状态：0 待还款 1 完结，-1 还款失败 · 可空 |
| `repay_channel` | varchar(10) | 还款渠道 · 可空 |
| `payment_no` | bigint(11) | 支付订单号 · 可空 |
| `repay_no` | varchar(32) | 还款流水号 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_payment_no`:payment_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
