---
id: tbl_fiserv_t_ping_url
object_type: Table
name: PING URL,如果向对应URL发起交易的时候超时,需要把UR (t_ping_url)
aliases: [t_ping_url, fiserv.t_ping_url]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: fiserv schema DDL
tags: [offline-business, fiserv]
sensitivity: normal
related_services: []
---

# PING URL,如果向对应URL发起交易的时候超时,需要把UR (t_ping_url)

## 用途
物理表 `fiserv.t_ping_url`,主键 `id`。PING URL,如果向对应URL发起交易的时候超时,需要把UR。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 自增ID · 可空 |
| `reg_id` | bigint | T_REGISTRATION表的ID · 可空 |
| `url` | varchar(255) | PING URL · 可空 |
| `ping_time_ms` | int | PING response time (ms) · 可空 |
| `response_time_ms` | int | HTTP请求响应时间 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_tpu_reg_id`:reg_id
- `idx_tpu_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
