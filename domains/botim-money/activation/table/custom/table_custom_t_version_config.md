---
id: tbl_custom_t_version_config
object_type: Table
name: 版本配置 (t_version_config)
aliases: [t_version_config, custom.t_version_config]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: custom schema DDL
tags: [activation, custom]
sensitivity: normal
related_services: []
---

# 版本配置 (t_version_config)

## 用途
物理表 `custom.t_version_config`,主键 `version_id`。版本配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `version_id` | int | 主键 · 可空 |
| `platform_type` | varchar(20) | 平台类型:ALL,IOS,ANDROID,WEB,H5 |
| `host_app` | varchar(20) | 宿主平台:ALL,payby,totok,bootim |
| `min_version` | varchar(20) | 空表示不控制 · 可空 |
| `max_version` | varchar(20) | 空表示不控制 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`version_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
