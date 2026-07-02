---
id: tbl_cregister_t_register_config
object_type: Table
name: Merchant Registration Configuration (t_register_config)
aliases: [t_register_config, cregister.t_register_config]
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

# Merchant Registration Configuration (t_register_config)

## 用途
物理表 `cregister.t_register_config`,主键 `id`。Merchant Registration Configuration。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Primary Key ID · 可空 |
| `fund_provider_code` | varchar(24) | Channel Provider |
| `inst_code` | varchar(24) | Institution Code |
| `fund_channel_code` | varchar(24) | Channel Code |
| `query_cron` | varchar(32) | Query Expression; Used to calculate the next execution time · 可空 |
| `batch_flag` | varchar(1) | Batch Flag; Y/N |
| `batch_type` | varchar(12) | Batch Type; FILE, INTERFACE · 可空 |
| `register_mode` | char | Registration Mode; R: Real-time, T: Scheduled |
| `query_flag` | char | Query Flag; Y: Supports Query, N: Does Not Support Query, gmt_next_retry is empty when N · 可空 |
| `gmt_create` | timestamp | Creation Time |
| `gmt_modified` | timestamp | Update Time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
