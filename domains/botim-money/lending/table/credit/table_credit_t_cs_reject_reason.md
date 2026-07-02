---
id: tbl_credit_t_cs_reject_reason
object_type: Table
name: 拒绝原因展示表 (t_cs_reject_reason)
aliases: [t_cs_reject_reason, credit.t_cs_reject_reason]
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

# 拒绝原因展示表 (t_cs_reject_reason)

## 用途
物理表 `credit.t_cs_reject_reason`,主键 `id`。拒绝原因展示表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `rule` | varchar(64) | 策略 |
| `clarification` | varchar(255) | 策略说明 · 可空 |
| `data_from` | varchar(128) | 数据来源 |
| `risk_type` | varchar(128) | 风险类型 |
| `risk_level` | tinyint | 风险等级 1~5, 5为最高 |
| `display_reason` | varchar(255) | 展示拒绝原因 |
| `rank` | tinyint | 展示拒绝原因排序，1~5, 数字越小越先排 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
