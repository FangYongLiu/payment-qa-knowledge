---
id: tbl_eminstalment_t_profile
object_type: Table
name: 用户信息 (t_profile)
aliases: [t_profile, eminstalment.t_profile]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 用户信息 (t_profile)

## 用途
物理表 `eminstalment.t_profile`,主键 `id`。用户信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `mobile` | varchar(32) | 手机号 · 可空 |
| `user_id` | varchar(20) | 用户ID |
| `sex` | tinyint | 姓别 · 可空 |
| `birthday` | char(10) | 生日 · 可空 |
| `name` | varchar(200) | 姓名 · 可空 |
| `identity` | varchar(50) | 身份证 · 可空 |
| `identity_invalid_time` | char(10) | 失效时间 · 可空 |
| `nationality` | varchar(64) | 国籍 · 可空 |
| `occupation` | varchar(50) | 职业 · 可空 |
| `income` | varchar(100) | 收入 · 可空 |
| `salary_date` | tinyint(3) | 发薪日 · 可空 |
| `uae_during` | varchar(100) | uae 时长 · 可空 |
| `city` | varchar(20) | 联系方式中的居住城市 · 可空 |
| `address` | varchar(255) | 联系方式中的详细地址 · 可空 |
| `email` | varchar(32) | 联系邮箱 · 可空 |
| `create_time` | timestamp | 创建日期 |
| `last_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_user_id`:user_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
