---
id: tbl_reconciliation_t_invoice_auto_config
object_type: Table
name: Configuration of  Invoice Automation (t_invoice_auto_config)
aliases: [t_invoice_auto_config, reconciliation.t_invoice_auto_config]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# Configuration of  Invoice Automation (t_invoice_auto_config)

## 用途
物理表 `reconciliation.t_invoice_auto_config`,主键 `config_id`。Configuration of  Invoice Automation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | bigint | 待补 |
| `fund_channel_code` | varchar(32) | Channel Code |
| `fund_channel_name` | varchar(64) | Channel Name · 可空 |
| `biz_type` | varchar(4) | Business Type |
| `company` | varchar(128) | Company name · 可空 |
| `max_charge` | decimal(10, 4) | Maximum commission charge amount · 可空 |
| `charge_rate` | decimal(10, 6) | Commission charges deducted Rate · 可空 |
| `company_address` | varchar(255) | Company address for invoice template · 可空 |
| `vat_rate` | decimal(10, 6) | VAT commission deducted Rate · 可空 |
| `receiver` | varchar(255) | Receivers · 可空 |
| `invoice_template` | varchar(255) | Name of invoice template · 可空 |
| `status` | int(1) | Status: 0-Disabled 1-Enabled · 可空 |
| `create_by` | varchar(45) | Creator account · 可空 |
| `created_time` | timestamp | Create time · 可空 |
| `updated_by` | varchar(45) | Update user account · 可空 |
| `updated_time` | timestamp | Update time · 可空 |

## 主键 / 索引
- 主键:`config_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
