---
id: tbl_ufs_tb_user_account_relation
object_type: Table
name: 用户账户关系表 (tb_user_account_relation)
aliases: [tb_user_account_relation, ufs.tb_user_account_relation]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ufs schema DDL
tags: [infrastructure, ufs]
sensitivity: normal
related_services: []
---

# 用户账户关系表 (tb_user_account_relation)

## 用途
物理表 `ufs.tb_user_account_relation`,主键 `user_id, account_id`。用户账户关系表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `user_id` | int | 用户id |
| `account_id` | int | 账户id |
| `is_default` | varchar(1) | 是否默认 · 可空 |

## 主键 / 索引
- 主键:`user_id, account_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
