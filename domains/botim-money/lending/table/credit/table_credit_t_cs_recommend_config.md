---
id: tbl_credit_t_cs_recommend_config
object_type: Table
name: 推荐策略配置表 (t_cs_recommend_config)
aliases: [t_cs_recommend_config, credit.t_cs_recommend_config]
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

# 推荐策略配置表 (t_cs_recommend_config)

## 用途
物理表 `credit.t_cs_recommend_config`,主键 `id`。推荐策略配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | ID · 可空 |
| `recommend_type` | varchar(50) | recommend_type: pl_to_cn, cn_to_pl |
| `view_strategy` | varchar(30) | view_strategy: MAX_PERIOD, MIN_PERIOD, ALL_PERIOD, SPECIFIED_PERIOD |
| `process_strategies` | varchar(200) | process_strategies(spliter: comma): OPEN_CARD, INCREASE_LIMIT, DECREASE_LIMIT, FALLBACK_LIMIT, NOTICE_IN_APP |
| `strategy_options` | varchar(255) | strategy extra options（JSON） · 可空 |
| `enabled` | tinyint | enable: 1-valid, 0-invalid · 可空 |
| `version` | int | version(cas) |
| `create_time` | datetime | create_time · 可空 |
| `update_time` | datetime | update_time · 可空 |

## 主键 / 索引
- 主键:`id`
- `uniq_recommend_type`:recommend_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
