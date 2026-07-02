---
id: tbl_credit_t_cs_liveness_verification
object_type: Table
name: needFaceRecognition liveness verification records (t_cs_liveness_verification)
aliases: [t_cs_liveness_verification, credit.t_cs_liveness_verification]
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

# needFaceRecognition liveness verification records (t_cs_liveness_verification)

## 用途
物理表 `credit.t_cs_liveness_verification`,主键 `id`。needFaceRecognition liveness verification records。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | primary key · 可空 |
| `user_id` | varchar(20) | member id |
| `vendor` | varchar(16) | disbursement vendor e.g. BANK, ACCOUNT · 可空 |
| `liveness_required` | tinyint | 1=required, 0=not required |
| `requirement_reason` | varchar(64) | LivenessRequirementReasonEnum code |
| `match_score` | decimal(6, 4) | iban holder vs kyc name similarity when evaluated · 可空 |
| `created_time` | timestamp | created time · 可空 |
| `updated_time` | timestamp | updated time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
