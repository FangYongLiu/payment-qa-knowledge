---
id: tbl_cashdesk_t_group
object_type: Table
name: 商户组 (t_group)
aliases: [t_group, cashdesk.t_group]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cashdesk schema DDL
tags: [payment-tool, cashdesk]
sensitivity: normal
related_services: []
---

# 商户组 (t_group)

## 用途
物理表 `cashdesk.t_group`,主键 `group_id`。商户组。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `group_id` | bigint | 组id · 可空 |
| `group_name` | varchar(64) | 商户组名称 |
| `group_type` | varchar(16) | 商户组类型 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `memo` | varchar(128) | 备注 · 可空 |
| `gmt_modified` | timestamp | 修改时间 |
| `party_role` | varchar(16) | 参与方角色 · 可空 |

## 主键 / 索引
- 主键:`group_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
