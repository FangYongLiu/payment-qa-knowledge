---
id: tbl_collection_t_ia_phone_aduit
object_type: Table
name: 电话审核 (t_ia_phone_aduit)
aliases: [t_ia_phone_aduit, collection.t_ia_phone_aduit]
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

# 电话审核 (t_ia_phone_aduit)

## 用途
物理表 `collection.t_ia_phone_aduit`,主键 `id`。电话审核。业务语义细节**待补**(表结构来自 DDL)。

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
| `app_id` | varchar(64) | 进件id |
| `uid` | varchar(64) | 本数据id |
| `collection_uid` | varchar(64) | 分配id |
| `user_uid` | varchar(64) | 审核员 |
| `round` | tinyint(3) | 轮数 · 可空 |
| `type` | tinyint(3) | 类型1 本人 2联系人 3家属 · 可空 |
| `relative` | varchar(32) | 关系称呼 · 可空 |
| `status` | varchar(32) | 接通状态 · 可空 |
| `mobile` | varchar(32) | 手机号 · 可空 |
| `name` | varchar(64) | 名称 · 可空 |
| `aware_of_loan` | varchar(20) | 意识到贷款 · 可空 |
| `willing_to_verify` | varchar(20) | 愿意核实 · 可空 |
| `reason_of_buying_phone` | varchar(20) | 购买手机的原因 · 可空 |
| `application_equipment` | varchar(20) | 应用设备 · 可空 |
| `model` | varchar(20) | 型号 · 可空 |
| `good_price` | varchar(20) | 价格 · 可空 |
| `term` | varchar(20) | 期限 · 可空 |
| `downpayment` | varchar(20) | 首付 · 可空 |
| `residence_address` | varchar(20) | 住址 · 可空 |
| `company_name` | varchar(20) | 公司名 · 可空 |
| `other_contacts` | varchar(20) | 其他联系人 · 可空 |
| `salary` | varchar(20) | 收入 · 可空 |
| `salary_date` | varchar(20) | 发薪日 · 可空 |
| `contact_name` | varchar(20) | 联系人姓名 · 可空 |
| `applicant` | varchar(20) | 借款人 · 可空 |
| `relation_ship` | varchar(20) | 关系 · 可空 |
| `random1` | varchar(50) | 随机问题1 · 可空 |
| `answer1` | varchar(50) | 问题1答案 · 可空 |
| `random2` | varchar(50) | 随机问题2 · 可空 |
| `answer2` | varchar(50) | 问题2答案 · 可空 |
| `random3` | varchar(50) | 随机问题3 · 可空 |
| `answer3` | varchar(50) | 问题3答案 · 可空 |
| `suspected_fraud` | varchar(500) | 涉嫌欺诈 · 可空 |
| `comment` | varchar(350) | 评价备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_application_id`:app_id
- `idx_collection_uid`:collection_uid
- `idx_uid`:uid
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
