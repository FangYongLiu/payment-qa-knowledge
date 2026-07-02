---
id: tbl_router_t_work_time
object_type: Table
name: work time (t_work_time)
aliases: [t_work_time, router.t_work_time]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: router schema DDL
tags: [payment-tool, router]
sensitivity: normal
related_services: []
---

# work time (t_work_time)

## 用途
物理表 `router.t_work_time`,主键 `id`。work time。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | unique id · 可空 |
| `work_time_type` | varchar(16) | work time type |
| `cron_expression` | varchar(32) | cron expression |
| `priority` | int(3) | priority |
| `last_time` | char(8) | hhmmss · 可空 |
| `enable` | char | Y/N |
| `extension` | varchar(255) | extension filed · 可空 |
| `gmt_create` | timestamp | create time |
| `gmt_update` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_twt_gct`:gmt_create

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
