---
id: tbl_authtoken_t_topic_config_dmk_param
object_type: Table
name: i18message参数 (t_topic_config_dmk_param)
aliases: [t_topic_config_dmk_param, authtoken.t_topic_config_dmk_param]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: authtoken schema DDL
tags: [activation, authtoken]
sensitivity: normal
related_services: []
---

# i18message参数 (t_topic_config_dmk_param)

## 用途
物理表 `authtoken.t_topic_config_dmk_param`,主键 `id, pkey`。i18message参数。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `pkey` | varchar(200) | 键 |
| `value` | varchar(200) | 值 |

## 主键 / 索引
- 主键:`id, pkey`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
