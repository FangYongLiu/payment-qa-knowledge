---
id: tbl_exchange_t_exchange_config
object_type: Table
name: 换汇系统配置唯一索引 (t_exchange_config)
aliases: [t_exchange_config, exchange.t_exchange_config]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: exchange schema DDL
tags: [payment-core, exchange]
sensitivity: normal
related_services: []
---

# 换汇系统配置唯一索引 (t_exchange_config)

## 用途
物理表 `exchange.t_exchange_config`,主键 `config_id`。换汇系统配置唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | int | 配置ID · 可空 |
| `config_type` | varchar(32) | 参数配置所属类型 |
| `config_key` | varchar(32) | 参数key |
| `config_value` | varchar(512) | 参数value · 可空 |
| `status` | char | 状态Y / N · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`config_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
