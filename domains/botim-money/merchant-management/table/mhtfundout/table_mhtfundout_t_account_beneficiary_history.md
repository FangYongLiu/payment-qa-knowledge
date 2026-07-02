---
id: tbl_mhtfundout_t_account_beneficiary_history
object_type: Table
name: 账号收益人历史表 (t_account_beneficiary_history)
aliases: [t_account_beneficiary_history, mhtfundout.t_account_beneficiary_history]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mhtfundout schema DDL
tags: [merchant-management, mhtfundout]
sensitivity: normal
related_services: []
---

# 账号收益人历史表 (t_account_beneficiary_history)

## 用途
物理表 `mhtfundout.t_account_beneficiary_history`,主键 `id`。账号收益人历史表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `member_id` | varchar(50) | 受益人mid |
| `partner_id` | varchar(50) | partnerId |
| `full_name_ues_token` | varchar(200) | 姓名摘要 · 可空 |
| `full_name_mask_text` | varchar(200) | 姓名掩码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `last_used_time` | timestamp(3) | 最后使用时间 |
| `account_type` | varchar(32) | accountType · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_abh_pm`:member_id, partner_id (UNIQUE)
- `i_abh_ct`:created_time
- `i_abh_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
