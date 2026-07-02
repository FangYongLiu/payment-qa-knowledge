---
id: tbl_mss_t_marketing_rule
object_type: Table
name: 限制规则表 (t_marketing_rule)
aliases: [t_marketing_rule, mss.t_marketing_rule]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 限制规则表 (t_marketing_rule)

## 用途
物理表 `mss.t_marketing_rule`,主键 `id`。限制规则表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 |
| `create_time` | timestamp | 创建时间 |
| `remarks` | varchar(128) | 备注 · 可空 |
| `update_time` | timestamp | 更新时间 |
| `op` | varchar(32) | 规则操作符 · 可空 |
| `type` | varchar(32) | 规则类型 · 可空 |
| `value` | varchar(256) | 规则参数 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
