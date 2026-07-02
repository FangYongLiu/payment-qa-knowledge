---
id: tbl_basiscustomer_t_sys_login_log
object_type: Table
name: 登录记录 (t_sys_login_log)
aliases: [t_sys_login_log, basiscustomer.t_sys_login_log]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basiscustomer schema DDL
tags: [activation, basiscustomer]
sensitivity: normal
related_services: []
---

# 登录记录 (t_sys_login_log)

## 用途
物理表 `basiscustomer.t_sys_login_log`,主键 `login_log_id`。登录记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `login_log_id` | bigint | 主键 · 可空 |
| `log_name` | varchar(64) | 日志名称 · 可空 |
| `user_id` | bigint | 管理员id · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `succeed` | varchar(8) | 是否执行成功 · 可空 |
| `message` | varchar(255) | 具体消息 · 可空 |
| `ip_address` | varchar(255) | 登录ip · 可空 |

## 主键 / 索引
- 主键:`login_log_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
