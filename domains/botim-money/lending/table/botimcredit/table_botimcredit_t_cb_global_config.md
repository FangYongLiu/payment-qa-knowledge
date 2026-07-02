---
id: tbl_botimcredit_t_cb_global_config
object_type: Table
name: global config for easycash (t_cb_global_config)
aliases: [t_cb_global_config, botimcredit.t_cb_global_config]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimcredit schema DDL
tags: [lending, botimcredit]
sensitivity: normal
related_services: []
---

# global config for easycash (t_cb_global_config)

## 用途
物理表 `botimcredit.t_cb_global_config`,主键 `id`。global config for easycash。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | primary key · 可空 |
| `config_key` | varchar(30) | config key |
| `config_value` | varchar(100) | config value |
| `config_desc` | varchar(200) | config description · 可空 |
| `valid_flag` | varchar(10) | open flag, Y-config valid, N-config invalid |
| `ext` | varchar(50) | ext · 可空 |
| `created_time` | timestamp | creation time |
| `last_modified` | timestamp | last modified time |

## 主键 / 索引
- 主键:`id`
- `t_cb_global_config_uk_config_key`:config_key (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
