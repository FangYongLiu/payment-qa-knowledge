---
id: tbl_csimple_t_day_call
object_type: Table
name: 每日通话 (t_day_call)
aliases: [t_day_call, csimple.t_day_call]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: csimple schema DDL
tags: [card, csimple]
sensitivity: normal
related_services: []
---

# 每日通话 (t_day_call)

## 用途
物理表 `csimple.t_day_call`,主键 `id`。每日通话。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 · 可空 |
| `partner_id` | varchar(32) | 平台ID |
| `uid` | varchar(32) | 用户uid |
| `call_day` | date | 通话日期 |
| `call_count` | int | 通话次数 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_day_call_pid_uid`:partner_id, uid (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
