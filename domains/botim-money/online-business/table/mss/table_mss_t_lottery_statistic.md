---
id: tbl_mss_t_lottery_statistic
object_type: Table
name: 会员抽奖记录锁 (t_lottery_statistic)
aliases: [t_lottery_statistic, mss.t_lottery_statistic]
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

# 会员抽奖记录锁 (t_lottery_statistic)

## 用途
物理表 `mss.t_lottery_statistic`,主键 `id`。会员抽奖记录锁。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID · 可空 |
| `activity_id` | varchar(64) | 抽奖活动ID · 可空 |
| `member_id` | varchar(32) | 会员ID · 可空 |
| `lottery_count` | int | 参与抽奖次数 · 可空 |
| `lottery_amount` | decimal(10, 2) | 参与抽奖金额 · 可空 |
| `lottery_date` | timestamp | 参与抽奖日期 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 修改日期 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
