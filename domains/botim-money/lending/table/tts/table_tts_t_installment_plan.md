---
id: tbl_tts_t_installment_plan
object_type: Table
name: Installment plan (t_installment_plan)
aliases: [t_installment_plan, tts.t_installment_plan]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: tts schema DDL
tags: [lending, tts]
sensitivity: normal
related_services: []
---

# Installment plan (t_installment_plan)

## 用途
物理表 `tts.t_installment_plan`,主键 `plan_id`。Installment plan。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `plan_id` | bigint(21) | plan id |
| `plan_ref_no` | bigint(21) | plan ref no, mapping to ext · 可空 |
| `merchant_id` | varchar(20) | merchant id |
| `store_id` | varchar(20) | store id · 可空 |
| `card_no` | varchar(32) | card_no |
| `supplier_code` | varchar(5) | supplier: VISA/ |
| `amount` | decimal(20, 4) | amount |
| `currency` | char(3) | currency |
| `external_plan_id` | varchar(50) | external plan id, UUID |
| `seq_no` | smallint(10) | seq_no, from 0 to 9999 |
| `content` | varchar(512) | content |
| `gmt_create` | timestamp(3) | create time |

## 主键 / 索引
- 主键:`plan_id`
- `idx_ins_plan_create`:gmt_create
- `idx_ins_plan_ext_id`:external_plan_id
- `idx_ins_plan_ref_no`:plan_ref_no

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
