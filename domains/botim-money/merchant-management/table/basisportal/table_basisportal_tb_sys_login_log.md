---
id: tbl_basisportal_tb_sys_login_log
object_type: Table
name: login record (tb_sys_login_log)
aliases: [tb_sys_login_log, basisportal.tb_sys_login_log]
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

# login record (tb_sys_login_log)

## 用途
物理表 `basisportal.tb_sys_login_log`,主键 `login_log_id`。login record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `login_log_id` | bigint | primary key |
| `log_name` | varchar(32) | log name · 可空 |
| `user_id` | bigint | admin id · 可空 |
| `create_time` | timestamp | creation time · 可空 |
| `succeed` | varchar(10) | execution success · 可空 |
| `message` | text | specific message · 可空 |
| `ip_address` | varchar(40) | login ip · 可空 |

## 主键 / 索引
- 主键:`login_log_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
