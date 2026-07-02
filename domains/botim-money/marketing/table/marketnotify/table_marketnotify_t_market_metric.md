---
id: tbl_marketnotify_t_market_metric
object_type: Table
name: 营销活动推广指标 (t_market_metric)
aliases: [t_market_metric, marketnotify.t_market_metric]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketnotify schema DDL
tags: [marketing, marketnotify]
sensitivity: normal
related_services: []
---

# 营销活动推广指标 (t_market_metric)

## 用途
物理表 `marketnotify.t_market_metric`,主键 `id`。营销活动推广指标。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | ID · 可空 |
| `metric_name` | varchar(32) | 指标名称：指标名称 |
| `target_source` | varchar(64) | 数据表 |
| `target_total_count` | bigint | 目标数据记录数 · 可空 |
| `target_sent_count` | bigint | 目标送达数 · 可空 |
| `effect_value` | bigint | 指标值：指标统计值 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
