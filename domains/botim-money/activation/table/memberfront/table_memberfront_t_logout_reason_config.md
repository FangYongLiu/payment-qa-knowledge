---
id: tbl_memberfront_t_logout_reason_config
object_type: Table
name: 注销原因配置表 (t_logout_reason_config)
aliases: [t_logout_reason_config, memberfront.t_logout_reason_config]
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

# 注销原因配置表 (t_logout_reason_config)

## 用途
物理表 `memberfront.t_logout_reason_config`,主键 `id`。注销原因配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(25) | 主键 · 可空 |
| `type` | varchar(25) | 类型 · 可空 |
| `title` | varchar(512) | 简介 · 可空 |
| `description` | varchar(800) | 原因描述 · 可空 |
| `enable_flag` | varchar(5) | 是否可用 · 可空 |
| `seq_idx` | varchar(10) | 编排顺序 · 可空 |
| `partner_id` | varchar(25) | 平台ID · 可空 |
| `memo` | varchar(512) | 备注 · 可空 |
| `create_time` | timestamp | 建立时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
