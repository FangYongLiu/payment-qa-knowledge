---
id: tbl_credit_t_cs_profile
object_type: Table
name: 用户信息 (t_cs_profile)
aliases: [t_cs_profile, credit.t_cs_profile]
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

# 用户信息 (t_cs_profile)

## 用途
物理表 `credit.t_cs_profile`,主键 `id`。用户信息。业务语义细节**待补**(表结构来自 DDL)。

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
| `sex` | tinyint(2) | 姓别 |
| `name` | varchar(50) | 姓名 · 可空 |
| `nationality` | varchar(200) | 国籍 · 可空 |
| `area` | varchar(100) | 区域 · 可空 |
| `city` | varchar(20) | 城市 · 可空 |
| `address` | varchar(255) | 地址 · 可空 |
| `occupation` | varchar(50) | 职位 · 可空 |
| `compay_address` | varchar(255) | 公司地址 · 可空 |
| `income` | varchar(100) | 收入 · 可空 |
| `income_precisely` | varchar(20) | precisely income · 可空 |
| `mail` | varchar(255) | 邮箱 · 可空 |
| `loan_for` | varchar(100) | 借款用途 · 可空 |
| `station` | varchar(50) | 岗位 · 可空 |
| `emergency_contact` | json | 紧急联系人 · 可空 |
| `birthday` | varchar(10) | 生日 · 可空 |
| `first_name` | varchar(200) | 姓名 · 可空 |
| `last_name` | varchar(50) | 姓名 · 可空 |
| `back_photo` | varchar(100) | id前相片 · 可空 |
| `passport_no` | varchar(100) | 护照号 · 可空 |
| `front_photo` | varchar(100) | id后相片 · 可空 |
| `created_time` | timestamp | 创建日期 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |
| `is_logout` | tinyint(5) | 注销 · 可空 |
| `out_partner_id` | varchar(20) | 销户平台 · 可空 |
| `is_subscription_bill_mail` | varchar(10) | 是否订阅邮件帐单 · 可空 |
| `stay_period` | varchar(50) | 时长 · 可空 |
| `religion` | varchar(100) | 宗教 · 可空 |
| `is_show_leantech` | tinyint(5) | 是否展示大额 · 可空 |
| `is_show_instalment` | tinyint(5) | 是否展示分期 |
| `select_bill_start` | varchar(100) | 用户选择还款日 · 可空 |
| `risk_tag` | varchar(255) | risk tag · 可空 |
| `salary_date` | varchar(100) | 发薪日 · 可空 |
| `lang` | varchar(10) | 待补 · 可空 |
| `eid_expiry_date` | timestamp | eid expiry date · 可空 |
| `icp_update_date` | timestamp | icp update date · 可空 |
| `wallet_iban` | varchar(64) | user Virtual IBAN · 可空 |
| `living_expense` | varchar(50) | Living expense · 可空 |
| `botim_id` | varchar(100) | Botim ID · 可空 |
| `payment_method_prefer` | varchar(32) | default payment method · 可空 |
| `tip_is_read` | tinyint(1) | homepage tooltips read status: 1 read 2 not read |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id (UNIQUE)
- `i_cs_profile_identity`:identity
- `i_cs_profile_mobile`:mobile

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
