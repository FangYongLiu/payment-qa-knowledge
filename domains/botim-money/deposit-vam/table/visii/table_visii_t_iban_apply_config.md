---
id: tbl_visii_t_iban_apply_config
object_type: Table
name: IBAN apply config (t_iban_apply_config)
aliases: [t_iban_apply_config, visii.t_iban_apply_config]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: visii schema DDL
tags: [deposit-vam, visii]
sensitivity: normal
related_services: []
---

# IBAN apply config (t_iban_apply_config)

## 用途
物理表 `visii.t_iban_apply_config`,主键 `config_id`。IBAN apply config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | int | config id · 可空 |
| `bank_code` | varchar(5) | PAYBY-Payby |
| `iban_type` | varchar(2) | iban type: P-Personal, C-Company |
| `bban` | varchar(20) | starting BBAN number |
| `apply_num` | int | number of IBANs to apply |
| `bank_entity_id` | varchar(10) | bank entity id |
| `status` | char | A-Active, D-Disabled |
| `gmt_create` | timestamp | create time · 可空 |
| `gmt_modified` | timestamp | modify time · 可空 |
| `memo` | varchar(64) | memo · 可空 |

## 主键 / 索引
- 主键:`config_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
