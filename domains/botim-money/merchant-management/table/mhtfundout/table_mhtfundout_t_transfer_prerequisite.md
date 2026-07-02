---
id: tbl_mhtfundout_t_transfer_prerequisite
object_type: Table
name: transfer prerequisite (t_transfer_prerequisite)
aliases: [t_transfer_prerequisite, mhtfundout.t_transfer_prerequisite]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mhtfundout schema DDL
tags: [merchant-management, mhtfundout]
sensitivity: normal
related_services: []
---

# transfer prerequisite (t_transfer_prerequisite)

## 用途
物理表 `mhtfundout.t_transfer_prerequisite`,主键 `id`。transfer prerequisite。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `currency_code` | char(3) | currencyCode |
| `transfer_type` | varchar(50) | transferType |
| `minimum_amount` | decimal(19, 4) | minimum amount |
| `created_time` | timestamp(3) | created time |
| `last_updated_time` | timestamp(3) | last updated time |
| `data_version` | bigint | data version |

## 主键 / 索引
- 主键:`id`
- `uk_tp_ct`:currency_code, transfer_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
