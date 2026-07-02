---
id: tbl_ppc_t_card_config
object_type: Table
name: Card Config (t_card_config)
aliases: [t_card_config, ppc.t_card_config]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Card Config (t_card_config)

## 用途
物理表 `ppc.t_card_config`,主键 `config_id`。Card Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | bigint | Config ID · 可空 |
| `virtual_card_id` | bigint | Virtual Card ID |
| `config_code` | varchar(50) | Config Code |
| `config_value` | varchar(100) | Config Value |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`config_id`
- `uk_card_config_code`:virtual_card_id, config_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
