---
id: tbl_npss_t_user_history
object_type: Table
name: 用户历史表 (t_user_history)
aliases: [t_user_history, npss.t_user_history]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# 用户历史表 (t_user_history)

## 用途
物理表 `npss.t_user_history`,主键 `history_id`。用户历史表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `history_id` | bigint(17) | 历史id |
| `member_id` | varchar(20) | 用户id |
| `name` | varchar(64) | 用户名 |
| `mobile_no` | varchar(20) | 手机号 · 可空 |
| `eid` | varchar(20) | eid · 可空 |
| `status` | char | 状态 · 可空 |
| `memo` | varchar(64) | 备注 · 可空 |
| `account_id` | bigint(17) | 账户id · 可空 |
| `iban` | varchar(23) | iban · 可空 |
| `currency` | char(3) | 币种 · 可空 |
| `app_id` | varchar(64) | app id · 可空 |
| `bank_account_id` | bigint(17) | 银行账户id · 可空 |
| `extension` | varchar(512) | Extension · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `gmt_history` | timestamp | 入库时间 · 可空 |

## 主键 / 索引
- 主键:`history_id`
- `idx_user_his_mid`:member_id, mobile_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
