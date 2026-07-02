---
id: tbl_memberfront_t_logout_check_config
object_type: Table
name: 校验项配置表 (t_logout_check_config)
aliases: [t_logout_check_config, memberfront.t_logout_check_config]
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

# 校验项配置表 (t_logout_check_config)

## 用途
物理表 `memberfront.t_logout_check_config`,主键 `id`。校验项配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(25) | 主键 · 可空 |
| `config_id` | int(10) | 服务配置ID · 可空 |
| `check_type` | varchar(25) | 校验项 · 可空 |
| `title` | varchar(255) | 标题 · 可空 |
| `icon` | varchar(355) | 图标 · 可空 |
| `content` | varchar(500) | 文案 · 可空 |
| `jump_msg` | varchar(50) | 跳转提示 · 可空 |
| `jump_url` | varchar(255) | 跳转链接 · 可空 |
| `status` | varchar(15) | 状态 · 可空 |
| `memo` | varchar(512) | 备注 · 可空 |
| `create_time` | timestamp | 建立时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
