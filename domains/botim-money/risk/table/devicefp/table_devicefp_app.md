---
id: tbl_devicefp_app
object_type: Table
name: app (app)
aliases: [app, devicefp.app]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: devicefp schema DDL
tags: [risk, devicefp]
sensitivity: normal
related_services: []
---

# app (app)

## 用途
物理表 `devicefp.app`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | app · 可空 |
| `name` | varchar(255) | app |
| `description` | varchar(255) | 待补 |
| `app_key` | varchar(255) | 待补 |
| `app_secret` | varchar(255) | app |
| `create_time` | timestamp | 待补 |
| `modify_time` | timestamp | 待补 |
| `package_name` | varchar(512) | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `un_app_key`:app_key (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
