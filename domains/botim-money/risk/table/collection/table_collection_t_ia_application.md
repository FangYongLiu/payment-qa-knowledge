---
id: tbl_collection_t_ia_application
object_type: Table
name: 信审进件表 (t_ia_application)
aliases: [t_ia_application, collection.t_ia_application]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 信审进件表 (t_ia_application)

## 用途
物理表 `collection.t_ia_application`,主键 `id`。信审进件表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(64) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(64) | 更新人员 · 可空 |
| `version_id` | smallint(5) | 乐观锁 · 可空 |
| `application_id` | varchar(64) | 进件id |
| `platform` | varchar(10) | 业务码 · 可空 |
| `task_name` | varchar(50) | 任务名 · 可空 |
| `member_id` | varchar(20) | 用户id |
| `order_no` | varchar(64) | 订单号 · 可空 |
| `ia_status` | tinyint(3) | 审核状态 · 可空 |
| `status` | tinyint(3) | 流转状态 · 可空 |
| `order_round` | tinyint(3) | 订单进件次数 · 可空 |
| `is_refuse` | tinyint(3) | 是否复审拒绝 · 可空 |
| `pho_round` | tinyint(3) | 电话呼叫轮数 · 可空 |
| `pho_end_time` | timestamp | 再次进入审核时间 · 可空 |
| `current_uid` | varchar(64) | 审核人员id · 可空 |
| `cur_inf_uid` | varchar(64) | 信息审核人员id · 可空 |
| `cur_pho_uid` | varchar(64) | 电话审核人员id · 可空 |
| `name` | varchar(150) | 借款人姓名 · 可空 |
| `mobile` | varchar(32) | 手机号 · 可空 |
| `identity` | varchar(64) | 证件号 · 可空 |
| `nationality` | varchar(64) | 国籍 · 可空 |
| `birthday` | varchar(20) | 生日 · 可空 |
| `company_name` | varchar(64) | 公司 · 可空 |
| `occupation` | varchar(64) | 职业 · 可空 |
| `monthly_salary` | varchar(64) | 月收入 · 可空 |
| `emergency_contact` | varchar(800) | 联系人 · 可空 |
| `user_note` | varchar(20) | sasleorder填写收入类型 · 可空 |
| `model` | varchar(50) | 型号 · 可空 |
| `amount` | decimal(15, 2) | 订单金额 · 可空 |
| `down_payment` | decimal(10, 2) | 首付金额 · 可空 |
| `term` | tinyint(3) | 期限 · 可空 |
| `residence_address` | varchar(255) | 住址 · 可空 |
| `salary_date` | tinyint(3) | 发薪日 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_application_id`:application_id
- `idx_current_uid`:current_uid
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
