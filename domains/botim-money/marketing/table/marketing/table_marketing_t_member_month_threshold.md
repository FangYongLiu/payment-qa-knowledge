---
id: tbl_marketing_t_member_month_threshold
object_type: Table
name: 会员奖励月阈值 (t_member_month_threshold)
aliases: [t_member_month_threshold, marketing.t_member_month_threshold]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketing schema DDL
tags: [marketing, marketing]
sensitivity: normal
related_services: []
---

# 会员奖励月阈值 (t_member_month_threshold)

## 用途
物理表 `marketing.t_member_month_threshold`,主键 `id`。会员奖励月阈值。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `member_id` | varchar(200) | 会员id |
| `scenario_code` | varchar(50) | 场景代码 |
| `month` | varchar(200) | 待补 |
| `reward_type` | varchar(200) | 待补 |
| `currency_code` | varchar(200) | 待补 |
| `threshold` | decimal(19, 4) | 阈值 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `uk_mmt`:member_id, scenario_code, month (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
