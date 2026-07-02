---
id: tbl_mss_t_lottery_award
object_type: Table
name: 奖品信息 (t_lottery_award)
aliases: [t_lottery_award, mss.t_lottery_award]
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

# 奖品信息 (t_lottery_award)

## 用途
物理表 `mss.t_lottery_award`,主键 `id`。奖品信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID · 可空 |
| `activity_id` | varchar(64) | 抽奖活动ID · 可空 |
| `award_type` | varchar(32) | 奖品类型 · 可空 |
| `award_name` | varchar(32) | 奖品名称 · 可空 |
| `award_count` | bigint | 奖品个数 · 可空 |
| `award_amount` | decimal(10, 2) | 奖品金额 · 可空 |
| `award_currency` | varchar(32) | 奖励币种 · 可空 |
| `award_weight` | bigint | 权重 |
| `memo` | varchar(64) | 备注 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 修改日期 · 可空 |
| `status` | varchar(32) | 状态 · 可空 |
| `award_odds` | decimal(4, 4) | 默认获胜率 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
