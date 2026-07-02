---
id: tbl_basisportal_t_external_system
object_type: Table
name: Systems registered in BMOC (t_external_system)
aliases: [t_external_system, basisportal.t_external_system]
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

# Systems registered in BMOC (t_external_system)

## 用途
物理表 `basisportal.t_external_system`,主键 `id`。Systems registered in BMOC。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `name_en` | varchar(64) | english name of system |
| `name_zh` | varchar(64) | chinese name · 可空 |
| `app_code` | varchar(32) | system identifier |
| `remarks` | varchar(255) | remarks · 可空 |
| `create_by` | varchar(45) | account of creator · 可空 |
| `create_time` | timestamp | create time · 可空 |
| `update_by` | varchar(45) | account of modifier · 可空 |
| `update_time` | timestamp | update time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
