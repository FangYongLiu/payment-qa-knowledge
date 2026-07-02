---
id: tbl_cregister_t_register_result
object_type: Table
name: Registration Result (t_register_result)
aliases: [t_register_result, cregister.t_register_result]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cregister schema DDL
tags: [merchant-management, cregister]
sensitivity: normal
related_services: []
---

# Registration Result (t_register_result)

## 用途
物理表 `cregister.t_register_result`,主键 `result_id`。Registration Result。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `result_id` | bigint | Primary Key ID; 8+9 |
| `register_id` | bigint | Registration Order Number |
| `inst_order_no` | varchar(100) | Institution Order Number |
| `inst_code` | varchar(24) | Institution Code |
| `fund_channel_code` | varchar(24) | Channel Code |
| `api_type` | varchar(12) | API Type |
| `inst_result_code` | varchar(32) | Unified Return Code · 可空 |
| `api_result_code` | varchar(32) | API Result Code · 可空 |
| `api_sub_result_code` | varchar(32) | API Result Sub Code · 可空 |
| `result_message` | varchar(100) | Result Message · 可空 |
| `status` | char | Status |
| `extension` | varchar(255) | Extension Information · 可空 |
| `memo` | varchar(100) | Remark · 可空 |
| `gmt_create` | timestamp | Creation Time |
| `gmt_modified` | timestamp | Update Time |

## 主键 / 索引
- 主键:`result_id`
- `idx_order_no`:inst_order_no
- `idx_reg_id`:register_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
