---
id: tbl_reconciliation_t_escrow_adjust_account
object_type: Table
name: Zand Escrow Adjust Account (t_escrow_adjust_account)
aliases: [t_escrow_adjust_account, reconciliation.t_escrow_adjust_account]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# Zand Escrow Adjust Account (t_escrow_adjust_account)

## 用途
物理表 `reconciliation.t_escrow_adjust_account`,主键 `account_id`。Zand Escrow Adjust Account。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_id` | bigint | Account Id · 可空 |
| `strategy_id` | bigint | Strategy Id |
| `account_type` | varchar(32) | Account Type |
| `account_name` | varchar(32) | Account Name |
| `account_identity` | varchar(32) | Account Identity |
| `enable_flag` | char | Enable Flag |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`account_id`
- `uk_strategy_type_account`:strategy_id, account_type, account_identity (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
