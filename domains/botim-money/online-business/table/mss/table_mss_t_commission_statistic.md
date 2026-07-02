---
id: tbl_mss_t_commission_statistic
object_type: Table
name: 推荐奖励统计表 (t_commission_statistic)
aliases: [t_commission_statistic, mss.t_commission_statistic]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 推荐奖励统计表 (t_commission_statistic)

## 用途
物理表 `mss.t_commission_statistic`,主键 `id`。推荐奖励统计表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `member_id` | varchar(20) | 奖励受益人 |
| `activity_code` | varchar(64) | 奖励活动 |
| `award_count` | int | 奖励笔数 · 可空 |
| `award_amount` | decimal(12, 4) | 奖励金额 · 可空 |
| `award_currency` | char(3) | 奖励币种 · 可空 |
| `award_type` | varchar(32) | 奖励类型 · 可空 |
| `award_level` | int | 奖励等级 · 可空 |
| `relation_commission` | decimal(12, 4) | 二级奖励 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `updated_time` | timestamp | 修改时间 · 可空 |
| `invitee_props` | varchar(200) | 被邀请人信息 · 可空 |
| `inviter_props` | varchar(200) | 邀请人信息 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_mid`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
