---
id: tbl_ons_t_data_sync_process
object_type: Table
name: 数据同步进度 (t_data_sync_process)
aliases: [t_data_sync_process, ons.t_data_sync_process]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ons schema DDL
tags: [infrastructure, ons]
sensitivity: normal
related_services: []
---

# 数据同步进度 (t_data_sync_process)

## 用途
物理表 `ons.t_data_sync_process`,主键 `id`。数据同步进度。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `match_config_id` | int | 匹配配置id · 可空 |
| `sync_begin_time` | timestamp | 开始时间 |
| `sync_end_time` | timestamp | 结束时间 |
| `interval_sec` | int | 时间片段秒数 |
| `delay` | int | 延迟时间 |
| `data_index` | int | 数据偏移下标 · 可空 |
| `page_size` | int | 分页每页大小 |
| `error_msg` | varchar(255) | 错误信息 · 可空 |
| `revison` | bigint | 版本 · 可空 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_match_config_id`:match_config_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
