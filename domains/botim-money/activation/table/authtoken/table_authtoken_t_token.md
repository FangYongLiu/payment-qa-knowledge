---
id: tbl_authtoken_t_token
object_type: Table
name: token (t_token)
aliases: [t_token, authtoken.t_token]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: authtoken schema DDL
tags: [activation, authtoken]
sensitivity: normal
related_services: []
---

# token (t_token)

## 用途
物理表 `authtoken.t_token`,主键 `id`。token。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 全局id |
| `token` | varchar(200) | code |
| `topic_id` | bigint | 持久化类型 |
| `status` | varchar(50) | 状态 |
| `member_id` | varchar(50) | 会员id |
| `scanner_partner_id` | varchar(50) | 扫码人平台id · 可空 |
| `token_partner_id` | varchar(50) | token平台id · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `rejected_code` | varchar(50) | 拒绝代码 · 可空 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_token`:token (UNIQUE)
- `idx_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
