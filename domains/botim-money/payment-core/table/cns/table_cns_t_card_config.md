---
id: tbl_cns_t_card_config
object_type: Table
name: Card Config (t_card_config)
aliases: [t_card_config, cns.t_card_config]
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

# Card Config (t_card_config)

## 用途
物理表 `cns.t_card_config`,主键 `config_id`。Card Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | int | Config ID · 可空 |
| `config_name` | varchar(100) | Config Name |
| `external_config_id` | varchar(50) | External Config ID |
| `external_template_id` | varchar(50) | External Template ID |
| `param_list` | varchar(200) | Param List · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `enable_flag` | char | Enable Flag: Y=Enable, N=Not Enable |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`config_id`
- `uk_external_config_id_template_id`:external_config_id, external_template_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
