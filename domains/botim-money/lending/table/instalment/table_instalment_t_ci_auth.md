---
id: tbl_instalment_t_ci_auth
object_type: Table
name: 认证状态表 (t_ci_auth)
aliases: [t_ci_auth, instalment.t_ci_auth]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: instalment schema DDL
tags: [lending, instalment]
sensitivity: normal
related_services: []
---

# 认证状态表 (t_ci_auth)

## 用途
物理表 `instalment.t_ci_auth`,主键 `id`。认证状态表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | 待补 · 可空 |
| `status` | smallint(5) | 1 认证成功 -1 认证失败 2 已过期 |
| `type` | smallint(5) | 认证类型: 1 工作签证 2 银行流水 3 劳工合同 |
| `user_id` | varchar(32) | 用户ID |
| `image1_key` | varchar(64) | file key · 可空 |
| `image2_key` | varchar(64) | file key · 可空 |
| `image3_key` | varchar(64) | file key · 可空 |
| `expired_time` | timestamp | 过期时间 · 可空 |
| `finish_time` | timestamp | 完成时间 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
