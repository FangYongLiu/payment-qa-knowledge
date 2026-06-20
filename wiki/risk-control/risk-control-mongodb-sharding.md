---
title: 风控MongoDB流水表分表(Sharding)改造
domain: risk-control
kind: wiki_page
slug: risk-control-mongodb-sharding
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1702953017
tags: []
---

# 风控MongoDB流水表分表(Sharding)改造

风控域针对 MongoDB 流水表 `t_payment_event` 与 `t_other_event` 启动的按年分表（Sharding）改造项目，用于支撑长期稳定运行、提升查询效率并实现水平扩展。

## 项目背景

- `t_payment_event` 与 `t_other_event` 是风控的 MongoDB 流水表。
- 数据量持续增长，需要通过分表实现分布式存储与高效管理。
- 改造方案：按年分表（Sharding），到达切换时间点后自动路由到分表。

## 相关配置参数

| 参数键 | 参数值示例 | 说明 |
| --- | --- | --- |
| `mongodb.sharding.cutoff-time` | `2026-01-07 07:50:00` | MongoDB 分表切换时间点；当前时间 > 此时间则自动使用分表 |
| `mongodb.sharding.tables` | `t_payment_event,t_other_event` | 需要分表的表 |
| `WIDE_TABLE_SYNC_SWITCH` | `Y` / `N` | 宽表同步开关：`Y`-开启，`N`-关闭；未配置默认开启 |
| `mongodb.sharding.test.force-mapping-table` | `true` / `false` | 强制使用映射表写入（仅供测试用） |

## 使用要点

- **切换时机**：以 `mongodb.sharding.cutoff-time` 为界，超过该时间点自动启用分表。
- **作用范围**：仅 `mongodb.sharding.tables` 中列出的表参与分表。
- **宽表同步**：通过 `WIDE_TABLE_SYNC_SWITCH` 控制，默认开启。
- **测试开关**：`mongodb.sharding.test.force-mapping-table` 仅供测试环境验证映射表写入逻辑使用，不应在生产开启。
