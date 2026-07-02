---
id: tbl_basisportal_tb_sys_relation
object_type: Table
name: role and menu relation table (tb_sys_relation)
aliases: [tb_sys_relation, basisportal.tb_sys_relation]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basisportal schema DDL
tags: [merchant-management, basisportal]
sensitivity: normal
related_services: []
---

# role and menu relation table (tb_sys_relation)

## 用途
物理表 `basisportal.tb_sys_relation`,主键 `relation_id`。role and menu relation table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `relation_id` | bigint | primary key |
| `menu_id` | bigint | menu id · 可空 |
| `role_id` | bigint | role id · 可空 |

## 主键 / 索引
- 主键:`relation_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
