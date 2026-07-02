---
id: tbl_cregister_t_visa_api_log
object_type: Table
name: t_visa_api_log (t_visa_api_log)
aliases: [t_visa_api_log, cregister.t_visa_api_log]
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

# t_visa_api_log (t_visa_api_log)

## 用途
物理表 `cregister.t_visa_api_log`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key |
| `inst_order_no` | varchar(64) | Request order number |
| `request_type` | varchar(20) | Request Type · 可空 |
| `request_body` | varchar(1024) | Request body · 可空 |
| `response_body` | varchar(1024) | Response body · 可空 |
| `status` | varchar(16) | Status (SUCCESS, FAILURE, ERROR) · 可空 |
| `gmt_create` | timestamp | Created time |
| `gmt_modified` | timestamp | Modified time |

## 主键 / 索引
- 主键:`id`
- `idx_gmt_create`:gmt_create
- `idx_inst_order_no`:inst_order_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
