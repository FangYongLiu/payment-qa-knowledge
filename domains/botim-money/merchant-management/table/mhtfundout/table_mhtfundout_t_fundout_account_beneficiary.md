---
id: tbl_mhtfundout_t_fundout_account_beneficiary
object_type: Table
name: 出款到账户子表 (t_fundout_account_beneficiary)
aliases: [t_fundout_account_beneficiary, mhtfundout.t_fundout_account_beneficiary]
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

# 出款到账户子表 (t_fundout_account_beneficiary)

## 用途
物理表 `mhtfundout.t_fundout_account_beneficiary`,主键 `id`。出款到账户子表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `member_id` | varchar(50) | 受益人mid · 可空 |
| `mobile_ues_token` | varchar(200) | 手机号ues_token · 可空 |
| `mobile_sha256_hex` | varchar(200) | 手机号摘要 · 可空 |
| `full_name_sha256_hex` | varchar(200) | 姓名ues_token · 可空 |
| `full_name_ues_token` | varchar(200) | 姓名摘要 · 可空 |
| `mobile_mask_text` | varchar(200) | 手机号掩码 · 可空 |
| `full_name_mask_text` | varchar(200) | 姓名掩码 · 可空 |
| `member_identity_pid` | varchar(32) | pid · 可空 |
| `member_identity_type` | varchar(32) | type · 可空 |
| `member_identity_value` | varchar(32) | value · 可空 |
| `account_type` | varchar(32) | accountType · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
