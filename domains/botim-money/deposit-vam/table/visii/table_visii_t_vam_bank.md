---
id: tbl_visii_t_vam_bank
object_type: Table
name: Vis bank (t_vam_bank)
aliases: [t_vam_bank, visii.t_vam_bank]
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

# Vis bank (t_vam_bank)

## 用途
物理表 `visii.t_vam_bank`,主键 `bank_code`。Vis bank。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `bank_code` | varchar(5) | bank code: ZAND/PAYBY |
| `bank_name` | varchar(32) | bank name: Zand LTC · 可空 |
| `status` | char | status,A-Available,U-Unavailable |
| `swift_code` | char(8) | swift code BANKAEAA |
| `routing_number` | varchar(32) | routing number · 可空 |
| `entity_id` | char(3) | entity_id · 可空 |
| `inst_code` | varchar(8) | inst code · 可空 |
| `subject` | varchar(32) | deposit subject · 可空 |
| `pool_mid` | varchar(20) | pool member id · 可空 |
| `wait_account` | varchar(32) | wait  account · 可空 |
| `bank_account` | varchar(32) | bank account · 可空 |
| `suspense_account` | varchar(32) | suspense account · 可空 |
| `address` | varchar(255) | bank address · 可空 |
| `gmt_create` | timestamp | create time · 可空 |
| `gmt_modified` | timestamp | modify time · 可空 |
| `memo` | varchar(64) | memo · 可空 |

## 主键 / 索引
- 主键:`bank_code`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
