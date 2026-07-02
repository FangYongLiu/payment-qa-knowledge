---
id: tbl_credit_t_cs_repay_wallet_apply
object_type: Table
name: repay bank transfer wallet apply request (t_cs_repay_wallet_apply)
aliases: [t_cs_repay_wallet_apply, credit.t_cs_repay_wallet_apply]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# repay bank transfer wallet apply request (t_cs_repay_wallet_apply)

## 用途
物理表 `credit.t_cs_repay_wallet_apply`,主键 `id`。repay bank transfer wallet apply request。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `created_time` | timestamp | create time · 可空 |
| `last_modified` | timestamp | last modified · 可空 |
| `user_id` | varchar(20) | 用户ID |
| `order_no` | varchar(64) | 订单唯一ID |
| `status` | tinyint(5) | status -1:close 0:doing 1:finish |
| `type` | tinyint(5) | type |
| `end_time` | timestamp | end Time · 可空 |
| `target_amount` | decimal(10, 2) | target max amount |
| `transfer_amount` | decimal(10, 2) | current bank transfer amount |
| `iban` | varchar(64) | user Virtual IBAN · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_end_time`:end_time
- `idx_order_no`:order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
