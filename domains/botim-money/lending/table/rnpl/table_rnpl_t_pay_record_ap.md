---
id: tbl_rnpl_t_pay_record_ap
object_type: Table
name: pay record to broker (t_pay_record_ap)
aliases: [t_pay_record_ap, rnpl.t_pay_record_ap]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# pay record to broker (t_pay_record_ap)

## 用途
物理表 `rnpl.t_pay_record_ap`,主键 `id`。pay record to broker。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 待补 · 可空 |
| `order_no` | varchar(64) | order no |
| `ap_id` | int | t_tenant_pay_rent_plan id · 可空 |
| `type` | smallint | 待补 · 可空 |
| `amount` | decimal(15, 2) | amount |
| `currency` | char(3) | 待补 |
| `status` | smallint | status 0 waiting，1，submited， 2 success ，-2 failed |
| `start_time` | timestamp | start time |
| `finish_time` | timestamp | finish_time · 可空 |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |
| `comments` | varchar(255) | Comments · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_on`:order_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
