---
id: tbl_basisportal_tb_sys_role
object_type: Table
name: role table (tb_sys_role)
aliases: [tb_sys_role, basisportal.tb_sys_role]
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

# role table (tb_sys_role)

## 用途
物理表 `basisportal.tb_sys_role`,主键 `role_id`。role table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `role_id` | bigint | primary key |
| `pid` | bigint | parent role id · 可空 |
| `name` | varchar(64) | role name · 可空 |
| `description` | varchar(255) | description · 可空 |
| `sort` | int(8) | sort order · 可空 |
| `version` | int(8) | version · 可空 |
| `create_time` | timestamp | creation time · 可空 |
| `update_time` | timestamp | update time · 可空 |
| `create_user` | bigint | creator · 可空 |
| `update_user` | bigint | updater · 可空 |

## 主键 / 索引
- 主键:`role_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
