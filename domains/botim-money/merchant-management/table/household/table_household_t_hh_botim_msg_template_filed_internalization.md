---
id: tbl_household_t_hh_botim_msg_template_filed_internalization
object_type: Table
name: botim msg template filed internalization (t_hh_botim_msg_template_filed_internalization)
aliases: [t_hh_botim_msg_template_filed_internalization, household.t_hh_botim_msg_template_filed_internalization]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: household schema DDL
tags: [merchant-management, household]
sensitivity: normal
related_services: []
---

# botim msg template filed internalization (t_hh_botim_msg_template_filed_internalization)

## 用途
物理表 `household.t_hh_botim_msg_template_filed_internalization`,主键 `id`。botim msg template filed internalization。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `language_code` | varchar(2) | language |
| `field` | varchar(32) | field |
| `kind` | varchar(8) | day:default|last|next|1...31 |
| `context` | varchar(127) | context · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
