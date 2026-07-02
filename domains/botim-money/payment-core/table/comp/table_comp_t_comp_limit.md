---
id: tbl_comp_t_comp_limit
object_type: Table
name: 补偿限定 (t_comp_limit)
aliases: [t_comp_limit, comp.t_comp_limit]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: comp schema DDL
tags: [payment-core, comp]
sensitivity: normal
related_services: []
---

# 补偿限定 (t_comp_limit)

## 用途
物理表 `comp.t_comp_limit`,主键 `id`。补偿限定。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `limit_role` | varchar(32) | 限定用户角色 |
| `comp_type` | varchar(16) | 补偿类型 trade,market |
| `max_limit` | varchar(32) | 补偿上限 |
| `min_limit` | varchar(32) | 补偿下限 上下限相同时固定额度 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
