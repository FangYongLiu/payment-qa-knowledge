---
id: tbl_memberfront_t_batch_kyc_detail
object_type: Table
name: Kyc Info (t_batch_kyc_detail)
aliases: [t_batch_kyc_detail, memberfront.t_batch_kyc_detail]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: memberfront schema DDL
tags: [activation, memberfront]
sensitivity: normal
related_services: []
---

# Kyc Info (t_batch_kyc_detail)

## 用途
物理表 `memberfront.t_batch_kyc_detail`,主键 `id`。Kyc Info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID, 前8后9 |
| `batch_no` | bigint | Batch No |
| `eid` | varchar(32) | EID Number;加密 · 可空 |
| `mobile_no` | varchar(32) | Mobile No;加密 · 可空 |
| `eid_front` | varchar(255) | EID Front Pic · 可空 |
| `eid_back` | varchar(255) | EID Back Pic · 可空 |
| `face` | varchar(255) | Face Pic · 可空 |
| `status` | varchar(8) | Status INIT,PREPARED,REGISTER,KYCING,FAILED,SUCCEED |
| `member_id` | varchar(20) | Member ID · 可空 |
| `token` | varchar(64) | KYC Flow Token · 可空 |
| `unity_result_code` | varchar(64) | Unity Error Code · 可空 |
| `error_message` | varchar(255) | Error Message · 可空 |
| `create_time` | timestamp(3) | Create Time |
| `update_time` | timestamp(3) | Update Time |

## 主键 / 索引
- 主键:`id`
- `idx_batch_no`:batch_no
- `idx_token`:token
- `idx_update_time_batch_no`:update_time, batch_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
