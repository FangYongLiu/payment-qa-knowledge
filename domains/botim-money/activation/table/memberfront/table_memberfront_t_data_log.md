---
id: tbl_memberfront_t_data_log
object_type: Table
name: t_data_log (t_data_log)
aliases: [t_data_log, memberfront.t_data_log]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: memberfront schema DDL
tags: [activation, memberfront]
sensitivity: normal
related_services: []
---

# t_data_log (t_data_log)

## 用途
物理表 `memberfront.t_data_log`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 |
| `apply_id` | bigint | 申请id |
| `uid` | varchar(64) | 平台标识 · 可空 |
| `mobile` | varchar(64) | 手机号 · 可空 |
| `op_status` | varchar(32) | SUCCESS|FAIL · 可空 |
| `flow_name` | varchar(64) | 流程名 · 可空 |
| `create_time` | timestamp | 建立时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `error_code` | varchar(255) | 错误code · 可空 |
| `error_message` | varchar(255) | 错误信息 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
