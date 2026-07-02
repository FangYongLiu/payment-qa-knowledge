---
id: tbl_csc_t_log_stat
object_type: Table
name: 日志统计 (t_log_stat)
aliases: [t_log_stat, csc.t_log_stat]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: csc schema DDL
tags: [merchant-management, csc]
sensitivity: normal
related_services: []
---

# 日志统计 (t_log_stat)

## 用途
物理表 `csc.t_log_stat`,主键 `id`。日志统计。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID · 可空 |
| `begin_time` | timestamp | 开始时间 |
| `end_time` | timestamp | 结束时间 |
| `app_code` | varchar(64) | appCode |
| `api_code` | varchar(255) | apiCode |
| `return_code` | varchar(64) | return code · 可空 |
| `return_msg` | varchar(255) | 错误信息 · 可空 |
| `value_count` | int | 出现次数 |
| `latest_tid` | varchar(64) | 最新tid · 可空 |
| `status` | varchar(10) | 确认状态: I=初始状态，M=人工确认，R=重试成功 |
| `update_by` | varchar(32) | 修改人 · 可空 |
| `memo` | varchar(255) | 待补 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_begin_time`:begin_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
