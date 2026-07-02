---
id: tbl_instalment_t_ci_profile
object_type: Table
name: 用户信息 (t_ci_profile)
aliases: [t_ci_profile, instalment.t_ci_profile]
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

# 用户信息 (t_ci_profile)

## 用途
物理表 `instalment.t_ci_profile`,主键 `id`。用户信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `mobile` | varchar(32) | 手机号 · 可空 |
| `user_id` | varchar(32) | 用户ID |
| `bank_card` | varchar(50) | 银行卡 · 可空 |
| `identity_invalid_time` | varchar(10) | 失效时间 · 可空 |
| `identity` | varchar(50) | 身份证 · 可空 |
| `sex` | tinyint | 姓别 · 可空 |
| `name` | varchar(500) | 姓名 · 可空 |
| `nationality` | varchar(200) | 国籍 · 可空 |
| `area` | varchar(100) | 区域 · 可空 |
| `city` | varchar(20) | 城市 · 可空 |
| `address` | varchar(255) | 地址 · 可空 |
| `occupation` | varchar(50) | 职位 · 可空 |
| `compay_address` | varchar(255) | 公司地址 · 可空 |
| `income` | varchar(100) | 收入 · 可空 |
| `company` | varchar(255) | 公司名 · 可空 |
| `email` | varchar(100) | 邮箱 · 可空 |
| `loan_for` | varchar(100) | 借款用途 · 可空 |
| `station` | varchar(50) | 岗位 · 可空 |
| `emergency_contact` | varchar(1000) | 紧急联系人 · 可空 |
| `birthday` | varchar(10) | 生日 · 可空 |
| `created_time` | timestamp | 创建日期 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |
| `is_logout` | tinyint | 注销 · 可空 |
| `out_partner_id` | varchar(20) | 销户平台 · 可空 |
| `residence` | varchar(255) | 居住 · 可空 |
| `uae_during` | varchar(100) | uae 时长 · 可空 |
| `religion` | varchar(50) | 宗教 · 可空 |
| `salary_date` | tinyint(3) | 发薪日 · 可空 |
| `monthly_expense` | varchar(100) | 每月花销 · 可空 |
| `children` | varchar(20) | 孩子 · 可空 |
| `family_address` | varchar(255) | 家庭地址 · 可空 |
| `education` | varchar(100) | 教育等级 · 可空 |
| `marital_status` | varchar(20) | 婚姻状态 · 可空 |
| `building` | varchar(255) | 地址详情 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
