---
id: tbl_bill_t_view_file_config
object_type: Table
name: View File Config (t_view_file_config)
aliases: [t_view_file_config, bill.t_view_file_config]
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

# View File Config (t_view_file_config)

## 用途
物理表 `bill.t_view_file_config`,主键 `file_config_id`。View File Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `file_config_id` | bigint | View File Id · 可空 |
| `file_code` | varchar(10) | File Code |
| `biz_product_code` | varchar(10) | Business Product Code |
| `role` | varchar(32) | Role |
| `payment_type` | varchar(32) | Payment Type |
| `view_code` | varchar(64) | View Code |
| `template_file_path` | varchar(64) | Template File Path |
| `valid_period` | varchar(32) | Valid Period |
| `memo` | varchar(255) | Memo · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`file_config_id`
- `uk_fc_bpc_role_pt`:file_code, biz_product_code, role, payment_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
