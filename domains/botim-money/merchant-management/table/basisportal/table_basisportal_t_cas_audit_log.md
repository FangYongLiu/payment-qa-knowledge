---
id: tbl_basisportal_t_cas_audit_log
object_type: Table
name: cas audit table (t_cas_audit_log)
aliases: [t_cas_audit_log, basisportal.t_cas_audit_log]
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

# cas audit table (t_cas_audit_log)

## 用途
物理表 `basisportal.t_cas_audit_log`,主键 `aud_id`。cas audit table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `aud_id` | bigint | primary key |
| `aud_user` | varchar(100) | user account |
| `aud_client_ip` | varchar(15) | client IP address |
| `aud_server_ip` | varchar(15) | server IP address · 可空 |
| `aud_resource` | varchar(255) | requested resource · 可空 |
| `aud_action` | varchar(100) | action performed |
| `applic_cd` | varchar(5) | application code · 可空 |
| `aud_date` | timestamp | audit date |
| `aud_useragent` | varchar(255) | user agent · 可空 |
| `aud_locale` | varchar(10) | locale · 可空 |

## 主键 / 索引
- 主键:`aud_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
