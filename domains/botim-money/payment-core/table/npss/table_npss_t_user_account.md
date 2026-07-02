---
id: tbl_npss_t_user_account
object_type: Table
name: 用户账户iban唯一索引 (t_user_account)
aliases: [t_user_account, npss.t_user_account]
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

# 用户账户iban唯一索引 (t_user_account)

## 用途
物理表 `npss.t_user_account`,主键 `account_id`。用户账户iban唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_id` | bigint(17) | 账户id |
| `member_id` | varchar(20) | 会员id |
| `iban` | varchar(23) | iban账户 |
| `bank_code` | char(3) | bank code,  413 |
| `currency` | char(3) | 币种 |
| `status` | char | 账户状态 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `app_id` | varchar(64) | app id · 可空 |
| `bank_account_id` | bigint(17) | 银行账号id · 可空 |

## 主键 / 索引
- 主键:`account_id`
- `idx_user_acct_mid`:member_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
