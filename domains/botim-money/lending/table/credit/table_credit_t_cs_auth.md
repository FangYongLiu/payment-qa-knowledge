---
id: tbl_credit_t_cs_auth
object_type: Table
name: 认证状态表 (t_cs_auth)
aliases: [t_cs_auth, credit.t_cs_auth]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# 认证状态表 (t_cs_auth)

## 用途
物理表 `credit.t_cs_auth`,主键 `id`。认证状态表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 待补 · 可空 |
| `status` | smallint(5) | 1 认证成功 -1 认证失败 2 已过期 |
| `auth_type` | smallint(5) | 认证类型: 1 邮箱 2 银行流水 |
| `user_id` | varchar(32) | 用户ID |
| `file1` | varchar(64) | 银行流水1 · 可空 |
| `file2` | varchar(64) | 银行流水2 · 可空 |
| `file3` | varchar(64) | 银行流水3 · 可空 |
| `mail_account` | varchar(64) | 邮箱帐号 · 可空 |
| `expired_time` | timestamp | 过期时间 · 可空 |
| `finish_time` | timestamp | 完成时间 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_user_id_created_time`:user_id, created_time
- `idx_mail_created`:mail_account, created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
