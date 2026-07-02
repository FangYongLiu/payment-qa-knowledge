---
id: tbl_memberfront_t_batch_kyc
object_type: Table
name: Batch Kyc (t_batch_kyc)
aliases: [t_batch_kyc, memberfront.t_batch_kyc]
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

# Batch Kyc (t_batch_kyc)

## 用途
物理表 `memberfront.t_batch_kyc`,主键 `batch_no`。Batch Kyc。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `batch_no` | bigint | Batch No |
| `list_path` | varchar(255) | KYC Excel Path |
| `photos_path` | varchar(255) | Photos Path |
| `status` | varchar(8) | Status PARSE,PREPARE,PROCESS,COMPLETE,FAILED |
| `total_count` | int | Total Count |
| `success_count` | int | Succeed Count |
| `fail_count` | int | Failed Count |
| `memo` | varchar(512) | Memo · 可空 |
| `unity_result_code` | varchar(64) | Unity Result Code · 可空 |
| `error_message` | varchar(255) | Error Message · 可空 |
| `create_user` | varchar(32) | Create User |
| `create_time` | timestamp(3) | Create Time |
| `update_time` | timestamp(3) | Update Time |

## 主键 / 索引
- 主键:`batch_no`
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
