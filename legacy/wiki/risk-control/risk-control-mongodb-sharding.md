---
title: 风控MongoDB流水表分表(Sharding)改造说明
domain: risk-control
kind: wiki_page
slug: risk-control-mongodb-sharding
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:cb5ac7b5-287b-4875-acc4-56419a74f05e
tags: []
---

# 风控MongoDB流水表分表(Sharding)改造说明

为保障风控流水表长期稳定运行、提升查询效率并支持水平扩展，对 MongoDB 中的 `t_payment_event`、`t_other_event` 两张流水表进行按年分表（Sharding）改造。

## 背景与目标

- 涉及表：`t_payment_event`、`t_other_event`（风控 MongoDB 流水表）
- 改造方式：按年分表（Sharding）
- 目标：分布式存储、高效管理、水平扩展、提升查询效率

## 切换机制

- 通过配置切换时间点 `mongodb.sharding.cutoff-time` 控制分表生效时机
- 当**当前时间 > 切换时间点**时，自动使用分表写入/查询
- 需要分表的表由 `mongodb.sharding.tables` 显式声明

## 相关配置参数

| 参数键 | 参数值示例 | 说明 |
| --- | --- | --- |
| `mongodb.sharding.cutoff-time` | `2026-01-07 07:50:00` | MongoDB 分表切换时间点；当前时间 > 此时间则自动使用分表 |
| `mongodb.sharding.tables` | `t_payment_event,t_other_event` | 需要分表的表清单 |
| `WIDE_TABLE_SYNC_SWITCH` | `Y` / `N` | 宽表同步开关：`Y`-开启，`N`-关闭；未配置时默认开启 |
| `mongodb.sharding.test.force-mapping-table` | `true` / `false` | 强制使用映射表写入（仅供测试用） |

## 注意事项

- `WIDE_TABLE_SYNC_SWITCH` 未配置时按"开启"处理
- `mongodb.sharding.test.force-mapping-table` 仅限测试场景使用，生产请勿开启
