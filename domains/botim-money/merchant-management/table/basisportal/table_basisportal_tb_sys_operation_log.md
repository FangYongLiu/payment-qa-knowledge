---
id: tbl_basisportal_tb_sys_operation_log
object_type: Table
name: operation log (tb_sys_operation_log)
aliases: [tb_sys_operation_log, basisportal.tb_sys_operation_log]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basisportal schema DDL
tags: [merchant-management, basisportal]
sensitivity: normal
related_services: []
---

# operation log (tb_sys_operation_log)

## 用途
物理表 `basisportal.tb_sys_operation_log`,主键 `operation_log_id`。operation log。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `operation_log_id` | bigint | primary key |
| `log_type` | varchar(32) | log type (dictionary) · 可空 |
| `log_name` | varchar(128) | log name · 可空 |
| `user_id` | bigint(65) | user id · 可空 |
| `class_name` | varchar(255) | class name · 可空 |
| `method` | varchar(32) | method name · 可空 |
| `create_time` | timestamp | creation time · 可空 |
| `succeed` | varchar(16) | execution success (dictionary) · 可空 |
| `message` | text | specific message · 可空 |
| `menu_id` | bigint | menu ID · 可空 |

## 主键 / 索引
- 主键:`operation_log_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
