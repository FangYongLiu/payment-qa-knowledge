---
id: tbl_visii_t_iban_apply
object_type: Table
name: Iban apply (t_iban_apply)
aliases: [t_iban_apply, visii.t_iban_apply]
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

# Iban apply (t_iban_apply)

## 用途
物理表 `visii.t_iban_apply`,主键 `apply_id`。Iban apply。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `apply_id` | int | Apply Id · 可空 |
| `request_no` | varchar(32) | Request No |
| `bank_code` | varchar(5) | Bank Code · 可空 |
| `apply_num` | smallint | Apply Num |
| `response_num` | smallint | Response Num · 可空 |
| `request_type` | char | Request Type: N-New,M-Modify · 可空 |
| `status` | char | Status · 可空 |
| `response_code` | varchar(32) | Response code · 可空 |
| `gmt_create` | timestamp | Create Time |
| `gmt_modified` | timestamp | Modify Time · 可空 |

## 主键 / 索引
- 主键:`apply_id`
- `uk_iban_apply_batch_no`:request_no (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
