---
id: tbl_amlreport_tb_kyc_user_risk_rate
object_type: Table
name: kyc user (tb_kyc_user_risk_rate)
aliases: [tb_kyc_user_risk_rate, amlreport.tb_kyc_user_risk_rate]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: amlreport schema DDL
tags: [compliance, amlreport]
sensitivity: normal
related_services: []
---

# kyc user (tb_kyc_user_risk_rate)

## 用途
物理表 `amlreport.tb_kyc_user_risk_rate`,主键 `member_id`。kyc user。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `member_id` | varchar(20) | member id |
| `id_no` | varchar(20) | id no |
| `screen_result` | varchar(15) | screen result · 可空 |
| `status` | char | status I S F · 可空 |
| `create_time` | timestamp | create time · 可空 |
| `finish_time` | timestamp | finish time · 可空 |

## 主键 / 索引
- 主键:`member_id`
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
