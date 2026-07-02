---
id: tbl_cns_t_event_config
object_type: Table
name: Event Config (t_event_config)
aliases: [t_event_config, cns.t_event_config]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cns schema DDL
tags: [payment-core, cns]
sensitivity: normal
related_services: []
---

# Event Config (t_event_config)

## 用途
物理表 `cns.t_event_config`,主键 `config_id`。Event Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | bigint | Config ID · 可空 |
| `event_code` | varchar(50) | Event Code: Trigger Event |
| `predicate_expression` | varchar(1000) | Predicate: Expression · 可空 |
| `action` | char(2) | Action: AC=Add Card, RC=Remove Card |
| `card_config_id` | bigint | Card Config ID |
| `enable_flag` | char | Enable Flag: Y=Yes, N=No |
| `update_time` | timestamp | Update Time |
| `create_time` | timestamp | Create Time |

## 主键 / 索引
- 主键:`config_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
