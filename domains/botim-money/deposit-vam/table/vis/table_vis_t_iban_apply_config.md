---
id: tbl_vis_t_iban_apply_config
object_type: Table
name: Unique for iban apply config (t_iban_apply_config)
aliases: [t_iban_apply_config, vis.t_iban_apply_config]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: vis schema DDL
tags: [deposit-vam, vis]
sensitivity: normal
related_services: []
---

# Unique for iban apply config (t_iban_apply_config)

## 用途
物理表 `vis.t_iban_apply_config`,主键 `config_id`。Unique for iban apply config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | bigint(19) | Config id · 可空 |
| `bank_code` | varchar(5) | BankCode, FAB/PAYBY/ENBD |
| `business_code` | varchar(7) | 待补 |
| `currency` | char | 0-AED, 1-USD · 可空 |
| `account_type` | varchar(1) | 0-Individual, 1-Merchant · 可空 |
| `current_id` | int(7) | Current Id Value |
| `baseline` | int(7) | Storage Baseline, will apply if small then this. |
| `status` | char | A-Available, U-Unavailable, E-Exhausted |
| `memo` | varchar(255) | Memo · 可空 |
| `gmt_create` | timestamp | Create Time |
| `gmt_modified` | timestamp | Modify Time · 可空 |

## 主键 / 索引
- 主键:`config_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
