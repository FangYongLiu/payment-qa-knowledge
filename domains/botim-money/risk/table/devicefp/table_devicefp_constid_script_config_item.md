---
id: tbl_devicefp_constid_script_config_item
object_type: Table
name: constid_script_config_item (constid_script_config_item)
aliases: [constid_script_config_item, devicefp.constid_script_config_item]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: devicefp schema DDL
tags: [risk, devicefp]
sensitivity: normal
related_services: []
---

# constid_script_config_item (constid_script_config_item)

## 用途
物理表 `devicefp.constid_script_config_item`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `config_id` | int | 待补 |
| `script` | text | 待补 · 可空 |
| `choose_field` | text | 待补 · 可空 |
| `code_name_map` | text | 待补 · 可空 |
| `type` | tinyint | 待补 |
| `status` | tinyint | 待补 |
| `error_msg` | text | 待补 · 可空 |
| `modify_time` | datetime | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
