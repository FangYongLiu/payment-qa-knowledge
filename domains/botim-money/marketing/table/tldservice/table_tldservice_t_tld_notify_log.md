---
id: tbl_tldservice_t_tld_notify_log
object_type: Table
name: tld notify log (t_tld_notify_log)
aliases: [t_tld_notify_log, tldservice.t_tld_notify_log]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: tldservice schema DDL
tags: [marketing, tldservice]
sensitivity: normal
related_services: []
---

# tld notify log (t_tld_notify_log)

## 用途
物理表 `tldservice.t_tld_notify_log`,主键 `id`。tld notify log。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `notify_order_id` | bigint | notifyOrderId |
| `response_code` | varchar(64) | responseCode · 可空 |
| `response_msg` | varchar(128) | responseCode · 可空 |
| `status` | varchar(16) | status |
| `created_time` | timestamp(3) | created_time |

## 主键 / 索引
- 主键:`id`
- `i_tnl_noi`:notify_order_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
