---
id: tbl_custom_t_decorate
object_type: Table
name: t_decorate (t_decorate)
aliases: [t_decorate, custom.t_decorate]
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

# t_decorate (t_decorate)

## 用途
物理表 `custom.t_decorate`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | id · 可空 |
| `decorate_type` | varchar(32) | 属性类型 · 可空 |
| `item_id` | bigint(18) | 定制项 · 可空 |
| `version_id` | int | 版本ID · 可空 |
| `title` | varchar(50) | 标题 · 可空 |
| `decorate_condition` | varchar(150) | 条件 · 可空 |
| `configure_format` | varchar(32) | 配置类型 · 可空 |
| `configure` | varchar(500) | 配置项 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
