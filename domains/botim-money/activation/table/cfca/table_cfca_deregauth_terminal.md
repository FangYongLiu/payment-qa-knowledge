---
id: tbl_cfca_deregauth_terminal
object_type: Table
name: deregauth_terminal (deregauth_terminal)
aliases: [deregauth_terminal, cfca.deregauth_terminal]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cfca schema DDL
tags: [activation, cfca]
sensitivity: normal
related_services: []
---

# deregauth_terminal (deregauth_terminal)

## 用途
物理表 `cfca.deregauth_terminal`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `appid` | bigint(11) | 待补 |
| `authenticator_id` | varchar(10) | 待补 |
| `authenticator_version` | varchar(10) | 待补 · 可空 |
| `upv` | varchar(100) | 待补 |
| `create_time` | bigint(15) | 待补 |
| `keyid` | varchar(255) | 待补 |
| `public_key` | varchar(4000) | 待补 |
| `reg_counter` | bigint(11) | 待补 · 可空 |
| `sign_counter` | bigint(11) | 待补 · 可空 |
| `status` | bigint(1) | 待补 · 可空 |
| `tc_displaypngchar` | varchar(2048) | 待补 · 可空 |
| `username` | varchar(255) | 待补 |
| `uvi` | varchar(255) | 待补 · 可空 |
| `dn` | varchar(1024) | 待补 · 可空 |
| `user_cert` | varchar(4000) | 待补 · 可空 |
| `user_verification` | bigint(11) | 待补 · 可空 |
| `device_id` | varchar(255) | 待补 · 可空 |
| `auth_type` | varchar(20) | 待补 · 可空 |
| `lock_time` | bigint(15) | 待补 · 可空 |
| `cert_expired_time` | bigint(15) | 待补 · 可空 |
| `dereg_time` | bigint(15) | 待补 |

## 主键 / 索引
- 主键:`id`
- `IDX_DAUTH_TERMINAL_APPID`:appid
- `IDX_DAUTH_TERMINAL_PART_HASH`:username

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
