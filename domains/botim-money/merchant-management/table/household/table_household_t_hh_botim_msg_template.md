---
id: tbl_household_t_hh_botim_msg_template
object_type: Table
name: botim msg template (t_hh_botim_msg_template)
aliases: [t_hh_botim_msg_template, household.t_hh_botim_msg_template]
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

# botim msg template (t_hh_botim_msg_template)

## 用途
物理表 `household.t_hh_botim_msg_template`,主键 `id`。botim msg template。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `template_code` | varchar(32) | template code |
| `template_name` | varchar(32) | template name |
| `head_icon` | varchar(512) | head icon conf |
| `head_background_color` | varchar(255) | head background color json list |
| `card_type` | tinyint | card type |
| `middle_image` | varchar(512) | middle image conf |
| `middle_part_outline` | char | middle part outline |
| `middle_ground_color` | varchar(255) | middle ground color json list |
| `from_rich_text` | varchar(512) | from rich text |
| `to_rich_text` | varchar(512) | to rich text |
| `status` | varchar(10) | status: ENABLE|DISABLE |
| `create_at` | timestamp | created time |
| `update_at` | timestamp | updated time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
