---
id: tbl_promo_t_infr_payby_m2u_callback
object_type: Table
name: t_infr_payby_m2u_callback (t_infr_payby_m2u_callback)
aliases: [t_infr_payby_m2u_callback, promo.t_infr_payby_m2u_callback]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: promo schema DDL
tags: [marketing, promo]
sensitivity: normal
related_services: []
---

# t_infr_payby_m2u_callback (t_infr_payby_m2u_callback)

## 用途
物理表 `promo.t_infr_payby_m2u_callback`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `request_order_no` | varchar(32) | request order no |
| `order_no` | varchar(32) | order no |
| `payment_status` | varchar(30) | payment status · 可空 |
| `notify_id` | varchar(32) | notify id |
| `notify_time` | varchar(64) | notify time |
| `notify_timestamp` | bigint | notify timestamp |
| `status` | char(6) | status: UnSync|Sync |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
