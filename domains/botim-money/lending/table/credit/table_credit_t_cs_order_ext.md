---
id: tbl_credit_t_cs_order_ext
object_type: Table
name: 展期订单表 (t_cs_order_ext)
aliases: [t_cs_order_ext, credit.t_cs_order_ext]
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

# 展期订单表 (t_cs_order_ext)

## 用途
物理表 `credit.t_cs_order_ext`,主键 `id`。展期订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 主健 · 可空 |
| `user_id` | varchar(64) | 用户ID |
| `father_order_no` | varchar(64) | 父订单 |
| `periods` | smallint(5) | 期数 · 可空 |
| `source_order_no` | varchar(64) | 祖订单 |
| `fee` | decimal(15, 2) | 费用 · 可空 |
| `days` | smallint(5) | 天数 |
| `status` | varchar(20) | 状态 · 可空 |
| `source_period` | smallint(5) | 对源订单的期数 · 可空 |
| `cur_period` | smallint(5) | 对某一期展 · 可空 |
| `son_order_no` | varchar(64) | 子订单 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |
| `extend_type` | varchar(32) | EXTENSION/RESTRUCTURE/DEFERRAL · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_father_order_no`:father_order_no
- `idx_son_order_no`:son_order_no
- `idx_source_order_no`:source_order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
