---
id: tbl_botimcredit_t_cb_card_snapshot
object_type: Table
name: 用户额度快照 (t_cb_card_snapshot)
aliases: [t_cb_card_snapshot, botimcredit.t_cb_card_snapshot]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimcredit schema DDL
tags: [lending, botimcredit]
sensitivity: normal
related_services: []
---

# 用户额度快照 (t_cb_card_snapshot)

## 用途
物理表 `botimcredit.t_cb_card_snapshot`,主键 `id`。用户额度快照。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `user_id` | varchar(20) | 用户ID |
| `order_no` | varchar(64) | 字段名 |
| `credit` | varchar(1000) | 产品 |
| `screen` | varchar(32) | 场景: REPAY OR CREATE_ORDER |
| `created_time` | timestamp | 创建日期 · 可空 |
| `last_modified` | timestamp | 修改日期 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
