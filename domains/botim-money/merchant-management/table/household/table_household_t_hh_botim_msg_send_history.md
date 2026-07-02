---
id: tbl_household_t_hh_botim_msg_send_history
object_type: Table
name: botim msg send history (t_hh_botim_msg_send_history)
aliases: [t_hh_botim_msg_send_history, household.t_hh_botim_msg_send_history]
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

# botim msg send history (t_hh_botim_msg_send_history)

## 用途
物理表 `household.t_hh_botim_msg_send_history`,主键 `id`。botim msg send history。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `msg_id` | varchar(32) | msg id |
| `transfer_id` | varchar(32) | transfer id · 可空 |
| `template_code` | varchar(32) | template code |
| `from_uid` | varchar(32) | from uid |
| `to_uid` | varchar(32) | to uid |
| `status` | varchar(32) | status: SEND|FAILED|UPDATE |
| `create_at` | timestamp | created time |
| `update_at` | timestamp | updated time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
