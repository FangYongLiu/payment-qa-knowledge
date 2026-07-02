---
id: tbl_basiscustomer_t_audit_record
object_type: Table
name: 审核记录 (t_audit_record)
aliases: [t_audit_record, basiscustomer.t_audit_record]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basiscustomer schema DDL
tags: [activation, basiscustomer]
sensitivity: normal
related_services: []
---

# 审核记录 (t_audit_record)

## 用途
物理表 `basiscustomer.t_audit_record`,主键 `audit_id`。审核记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `audit_id` | bigint | 审核ID：前八后九 |
| `audit_type` | varchar(64) | 审核类型 |
| `location_mark` | varchar(32) | 定位标识 · 可空 |
| `applier` | varchar(32) | 申请人 |
| `abbreviation` | varchar(128) | 审核摘要 |
| `audit_info` | text | 审核信息 · 可空 |
| `audit_status` | char(3) | 审核状态：AW待申请，AF申请失败，W待审核，P通过，R拒绝 |
| `execute_status` | char | 执行状态：P处理中，S成功，F失败 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`audit_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
