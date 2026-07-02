---
id: tbl_reconciliation_t_reconciliation_config
object_type: Table
name: 对账综合配置表 (t_reconciliation_config)
aliases: [t_reconciliation_config, reconciliation.t_reconciliation_config]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 对账综合配置表 (t_reconciliation_config)

## 用途
物理表 `reconciliation.t_reconciliation_config`,主键 `id`。对账综合配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `config_key` | varchar(255) | 配置Key |
| `config_value` | text | 配置Value |
| `memo` | varchar(255) | 备注 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `unique_key`:config_key (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
