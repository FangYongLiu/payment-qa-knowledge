---
id: tbl_onboarding_t_aani_merchant_onboarding_request
object_type: Table
name: AANI merchant onboarding requests (t_aani_merchant_onboarding_request)
aliases: [t_aani_merchant_onboarding_request, onboarding.t_aani_merchant_onboarding_request]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: onboarding schema DDL
tags: [merchant-management, onboarding]
sensitivity: normal
related_services: []
---

# AANI merchant onboarding requests (t_aani_merchant_onboarding_request)

## 用途
物理表 `onboarding.t_aani_merchant_onboarding_request`,主键 `id`。AANI merchant onboarding requests。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `merchant_mid` | varchar(50) | Merchant MID to be onboarded |
| `created_date` | timestamp | When the request was created |
| `processed` | tinyint(1) | Whether this request has been processed |
| `processed_date` | timestamp | When the request was processed · 可空 |
| `status` | varchar(10) | 待补 |

## 主键 / 索引
- 主键:`id`
- `merchant_mid`:merchant_mid (UNIQUE)
- `uk_merchant`:merchant_mid (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
