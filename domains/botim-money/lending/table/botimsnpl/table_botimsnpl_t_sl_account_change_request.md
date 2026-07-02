---
id: tbl_botimsnpl_t_sl_account_change_request
object_type: Table
name: snpl account change request table (t_sl_account_change_request)
aliases: [t_sl_account_change_request, botimsnpl.t_sl_account_change_request]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# snpl account change request table (t_sl_account_change_request)

## 用途
物理表 `botimsnpl.t_sl_account_change_request`,主键 `id`。snpl account change request table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | unique id · 可空 |
| `old_user_id` | varchar(20) | old user id |
| `new_user_id` | varchar(20) | new user id |
| `new_mobile` | varchar(32) | new mobile |
| `applicant` | varchar(50) | applicant |
| `reason` | varchar(200) | reason |
| `status` | varchar(10) | PROCESSING/SUCCESS/FAILED |
| `error_description` | varchar(100) | error description · 可空 |
| `ext` | varchar(200) | ext · 可空 |
| `created_time` | datetime | created time |
| `last_modified` | datetime | last modified time |

## 主键 / 索引
- 主键:`id`
- `idx_acct_created_time`:created_time
- `idx_acct_new_user_id`:new_user_id
- `idx_acct_old_user_id`:old_user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
