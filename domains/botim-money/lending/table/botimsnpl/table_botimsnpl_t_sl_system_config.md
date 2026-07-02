---
id: tbl_botimsnpl_t_sl_system_config
object_type: Table
name: t_sl_system_config (t_sl_system_config)
aliases: [t_sl_system_config, botimsnpl.t_sl_system_config]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# t_sl_system_config (t_sl_system_config)

## 用途
物理表 `botimsnpl.t_sl_system_config`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `config_type` | varchar(30) | OVERDUE_TIP, PRODUCT_PRIORITY |
| `start_value` | int | start value · 可空 |
| `end_value` | int | end value · 可空 |
| `config_key` | varchar(100) | config key · 可空 |
| `config_value` | varchar(255) | config value · 可空 |
| `config_params` | varchar(255) | extend params · 可空 |
| `status` | tinyint | 1=valid，0=invalid · 可空 |
| `created_time` | timestamp | created time |
| `last_modified` | timestamp | last modified time |

## 主键 / 索引
- 主键:`id`
- `idx_sys_cfg_key`:config_key

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
