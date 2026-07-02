---
id: tbl_botimsnpl_t_sl_coupon_user
object_type: Table
name: t_sl_coupon_user (t_sl_coupon_user)
aliases: [t_sl_coupon_user, botimsnpl.t_sl_coupon_user]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# t_sl_coupon_user (t_sl_coupon_user)

## 用途
物理表 `botimsnpl.t_sl_coupon_user`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `campaign_code` | varchar(50) | campaign code |
| `coupon_code` | varchar(50) | coupon code |
| `user_id` | varchar(20) | user id |
| `status` | varchar(20) | UNUSED/APPLIED/USED/REFUND/EXPIRED |
| `current_campaign_id` | bigint | current campaign id · 可空 |
| `current_coupon_id` | bigint | current coupon id · 可空 |
| `channel_no` | varchar(50) | channel no · 可空 |
| `del_flag` | varchar(2) | Y-deleted, N-not deleted · 可空 |
| `ext` | varchar(255) | ext · 可空 |
| `created_time` | timestamp | created time |
| `last_modified` | timestamp | last modified time |

## 主键 / 索引
- 主键:`id`
- `idx_coupon_camp_coupon_code`:campaign_code, coupon_code
- `idx_coupon_remit_order_no`:channel_no
- `idx_coupon_user_created_time_status`:created_time, status
- `idx_coupon_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
