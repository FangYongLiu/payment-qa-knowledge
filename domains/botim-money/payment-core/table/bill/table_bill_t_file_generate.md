---
id: tbl_bill_t_file_generate
object_type: Table
name: File Generate (t_file_generate)
aliases: [t_file_generate, bill.t_file_generate]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bill schema DDL
tags: [payment-core, bill]
sensitivity: normal
related_services: []
---

# File Generate (t_file_generate)

## 用途
物理表 `bill.t_file_generate`,主键 `id`。File Generate。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 |
| `request_no` | varchar(32) | Request Number |
| `client_id` | varchar(32) | Client Id |
| `file_code` | varchar(32) | File Code |
| `period_type` | char | Period Type: M=Month,D=Day |
| `begin_str` | varchar(20) | Begin String |
| `end_str` | varchar(20) | End String |
| `member_id` | varchar(20) | Member Id |
| `file_name` | varchar(64) | File Name · 可空 |
| `file_url` | varchar(256) | File Url · 可空 |
| `file_size` | bigint | File Size · 可空 |
| `status` | char | Status: P=Processing,S=Success |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- `uk_requestno_client_filecode`:request_no, client_id, file_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
