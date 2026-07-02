---
id: tbl_gpoint_t_account_change_log
object_type: Table
name: 账户变更日志 (t_account_change_log)
aliases: [t_account_change_log, gpoint.t_account_change_log]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: gpoint schema DDL
tags: [marketing, gpoint]
sensitivity: normal
related_services: []
---

# 账户变更日志 (t_account_change_log)

## 用途
物理表 `gpoint.t_account_change_log`,主键 `log_id`。账户变更日志。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `log_id` | bigint | 日志ID：前八后九 |
| `account_no` | bigint(19) | 账户号 |
| `before_status` | varchar(10) | 前状态 |
| `after_status` | varchar(10) | 后状态 |
| `operator` | varchar(32) | 操作员 |
| `memo` | varchar(128) | 备注 · 可空 |
| `client_id` | varchar(32) | 客户端ID |
| `create_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`log_id`
- `idx_account_no_create_time`:create_time, account_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
